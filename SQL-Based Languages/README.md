# SQL Style Guide

For relational databases, Ignia works primarily in Transact SQL (T-SQL) via Microsoft SQL Server, although many of the guidelines below should apply to most SQL variants.

> *Note:* This style guide inherits rules from the [Global Style Guide](../README.md). This document supersedes our legacy [SQL Style Guide](../Legacy/SQL.StyleGuide.doc) and [SQL Standards](../Legacy/SQL.Standards.doc) documents (Microsoft Word).

## Contents
- [Identifiers](#identifiers)
  - [Columns](#columns)
- [Formatting](#formatting)
- [Design](#design)
- [Language Features](#language-features)
  - [Data Types](#data-types)
  - [Primary Keys](#primary-keys)
  - [Stored Procedures](#stored-procedures)
  - [Indexes](#indexes)
- [Acknowledgments](#acknowledgments)

## Identifiers
- Tables, views, and stored procedures should begin with a brief, `lowercase` namespace followed by an underscore to separate related objects (e.g., `account_Users`)
- Table and view names should be represented by pluralized `PascalCase` noun phrases representing the entity type (e.g., `account_Logins`, `content_Articles`)
- Views should be prefixed by `vw_` to clearly indicate that they are not writable (e.g., `vw_account_Logins`)
- Stored procedures should be named using a verb (e.g., `set`, `get`, `delete`) followed by a noun representing the entity type (e.g., `account_setUser`, `account_getLogins`, `content_deleteArticle`)
- Stored procedures should *not* be prefixed with `sp_`; this is reserved for system stored procedures, and influences database search order
- While permitted, object identifiers should not include periods, as this requires quoted identifiers to distinguish from SQL's object notation

### Columns
- Column names should be `PascalCase` and will typically be composed of singular nouns or noun phrases (e.g., `FirstName`, `Email`)
- Column names should map to their names in corresponding code wherever possible
  - The exception is foreign key constraints which may be abstracted to (collections of) references in code
- Consider prefixing column names with the singular entity type (e.g., `User`) *if* the column identifier is not otherwise unique (e.g., `ID`, `Name`) *and* it is likely to be joined with other tables with similar names (for this reason, identifiers should *always* include the entity name)
- Identity columns should begin with the singular entity name (e.g., `User`) followed by `ID` (e.g., `UserID`)
- Foreign key constraints should be identical to the primary key constraint they reference (e.g., `UserID`)
  - If a foreign key constraint represents a particular relationship, it should be prefixed by the relationship type and an underscore (e.g., `ApprovedBy_UserID`, `Announcement_ArticleID`)
- Bit fields should begin with a present indicative (e.g., `isEnabled`, `hasReplies`, etc.)
- Only use underscores in column names to distinguish *concepts*; do not use underscores to separate words
- Prefer beginning date fields with `Date` (e.g., `DateAdded`, `DateStart`, `DateEnd`)
- For collecting contact information, prefer the field names `Province` (over `State`) and `PostalCode` (over `ZipCode`) in anticipation of internationalization
- Columns representing URLs should end with `URL`
- Parameter names should generally correspond to column names unless they are intended exclusively for setting conditional logic (e.g., `@IsRecursive`)

## Formatting
- Use uppercase keywords (e.g., `SELECT`, `FROM`, `WHERE`)
- Use hard tab stops set to four characters, for consistency with SQL Studio and Visual Studio (this is the exception to Ignia's general code formatting rules)
- Align column names in queries to column 17 (16 characters indent), assignments to column 41 (40 character indent)
- Place one column, clause per line in queries
- For nested queries, place opening parenthesis next to the opening clause (e.g., `WHERE`, `AND`, `OR`); indent first line (but not column names or values) two spaces

```sql
SELECT          Username                ,
                Locale
FROM            account_Users           Users
WHERE (         @UserID                 = null
  OR            UserID                  = 1234
)
AND (
  SELECT        TOP 1
                Email
  FROM          account_Email           Email
  WHERE         Email.UserID            = Users.UserID
    AND         Type                    = 1
)
```

## Design
- Prefer highly normalized data structures; only denormalize data as required by optimization
  - To denormalize commonly requested sets, rely on views; these do not provide execution optimization, but do simplify otherwise complex queries by centralizing joins
- If there is a need for more than one related item (e.g., `primary_Street1`, `secondary_Street1`) consider establishing a secondary table for a 1:n relationship (even if the number of relations is expected to be constrained to a fixed number)
- For non-lookup tables, consider adding `DateAdded` and `DateUpdated` columns for basic auditing purposes
  - For advanced auditing (e.g., with `Source`, `Type`, `Explanation`), prefer a centralized auditing table (e.g., `audit_History`)
- Consider assigning a logical maximum limit to queries to prevent returning more data than the application is expected to use (e.g., `TOP 500`)
- Consider creating lookup tables (with foreign key constraints) to map to enumerators in order to enforce data integrity and optionally provide friendly lookups (via joins)

## Language Features
- Data access should be restricted to stored procedures *unless* using an O/RM (e.g., `Entity Framework`, `NHibernate`)
- For data persistence, prefer Code First approaches to Database First, but be aware of the schema it generates and aim to maintain consistency with Ignia's standards
- Avoid use of dynamic SQL, either via `exec`, or by string concatenation in client code; this does not yield efficient execution plans and can expose vulnerability to SQL injection attacks
- Avoid cursors and nested queries wherever possible, as these are not a performant way for querying set-based data; prefer joins
- For optional clauses, use the `where (@column is null or column = @column)` pattern
- Consider setting seeds based on the expected number of values to ensure consistent digits (e.g., for states, set seed to 10; for countries, 100; for users, 1,000,000); this can make the data easier to "eyeball"

### Data Types
- For columns storing user-collected data, consider using localized data types (e.g., `nvarchar`) unless it is *known* that content will be restricted exclusively to the Latin character set
- Carefully consider the length and precision of data types; do not blindly assign one-size-fits-most values (e.g., `varchar(100)` for profile fields)
- Avoid excessive use of custom data types; prefer when relying on a set data type definition across a broad set of objects

### Primary Keys
- In general, primary keys should use `int`; for lookup tables with a predictably small number of records (e.g., `lookup_States`), use `tinyint`
- Primary keys should *not* use `uniqueidentifier` unless it's absolutely necessary for the identity to be *globally unique* (e.g., it will be merged with remote data stores)
  - If records need a non-predictable public key, consider assigning a separate `PublicKey` field using `uniqueidentifier` for this purpose

### Stored Procedures
- When using stored procedures for data access, plan to have full "CRUD" coverage (e.g., `account_getUsers`, `account_setUser`, `account_deleteUser`)
  - Combine create and update operations into a single stored procedure prefixed with `set` (e.g., `account_setUser`)
    - If the primary key is null, perform an `insert`; otherwise, perform an `update`
- When setting predictable data for related tables, consider passing a concatenated array of values and splitting within the stored procedure
  - When the number of columns is large or unpredictable, prefer using a separate stored procedure
- Avoid returning multiple record sets per stored procedure, although there are cases where this is the best approach
- Prefer using return data via record sets; prefer using return values for status codes
  - For status codes, use negative numbers for errors; positive numbers for success; this makes it easy to predictably capture exceptions

### Indexes
- Establish indexes on unique keys that may not be part of the primary key (e.g., `Username` or `Email` for a `account_Users` table)
  - If queries consistently use a combination of fields in the query, use each column in the index (e.g., `Username`, `password`, `salt`)
- Consider regular (e.g., quarterly) analysis of indexes based on profile data to ensure indexes are well-tuned based on actual queries

## Comments
- A header with an inline history should be included for every stored procedure and user defined function
- Nesting should be limited within SQL scripts and, as such, only two tiers of comments are defined


```sql
--------------------------------------------------------------------------------------------------------------------------------
-- [NAME]
-- Purpose                      [Purpose]
-- Parameters
--   Input                      See Below
--   Output                     [Output Variable(s)]
--
-- History
--  [FName][LName]              MMDDYYYY                        [Update Description]
--------------------------------------------------------------------------------------------------------------------------------

--------------------------------------------------------------------------------------------------------------------------------
-- TIER 1 COMMENT
--------------------------------------------------------------------------------------------------------------------------------

-- Tier 2 comment

```

<!--
## Acknowledgments
-->