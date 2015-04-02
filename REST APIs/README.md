# REST API Style Guide

A primary focus of Ignia's is on developing APIs, be they class libraries or web services. While the two overlap in many core objectives, however, they differ in practical guidance, particularly when it comes to "RESTful" APIs. The following articulate Ignia's standards and principles for establishing web services that are both flexible as well as usable.

> *Note:* This style guide inherits rules from the [Global Style Guide](../README.md). It also shares certain fundamental concepts with the [C# Class Library Style Guide](../C-Based%20Languages/C%23/Class%20Libraries.md). Finally, since REST APIs tend to utilize JSON as a serialization format, this guide acknowledges best practices from the [JSON Style Guide](../C-Based%20Languages/JavaScript/JSON.md) - although, it is not expected that web service output will adhere to JSON formatting standards (due to file minification).

## Contents
- [Design](#design)
  - [Method Conventions](#method-conventions)
  - [URL Conventions](#url-conventions)
  - [Query String Conventions](#query-string-conventions)
  - [Body Conventions](#body-conventions)

<!--
- [Identifiers](#identifiers)
- [Language Features](#language-features)
  - [Authentication](#authentication)
- [Comments](#comments)
  - [Documentation](#documentation)
- [Acknowledgments](#acknowledgments)
-->

## Design

### Overview
The following is a broad overview of how different concepts map to different HTTP components; each of these will be covered in more depth below.

| Concept       | HTTP Location | Example(s)
| --------------|---------------|---------------------------------------------------------------
| Action        | Method        | `GET`, `POST`, `PUT`, `PATCH`
| Collection    | URL           | `/Books`
| Entity        | URL           | `/Books/Ficciones`
| Query         | Query String  | `/Authors?$top=10&$skip=30&orderBy=LastName`
| Content       | Body          | `{ 'name': 'Ficcionnes', 'Author': 'Jorge Luis Borges' }`

### Method Conventions

> *Important:* Methods should be used as the primary means of triggering actions; always prefer methods to URL conventions or query string parameters for defining actions.

- Standard create, read, update, and delete (CRUD) actions should be defined using HTTP methods (i.e., `POST` for create) with content being set using the HTTP body
- Prefer the standard HTTP methods (e.g., `GET`, `POST`, `PUT`, `DELETE`, `HEAD`, etc); avoid establishing custom HTTP actions (e.g., `CREATE`, `UPDATE`, `LIST`)
- HTTP methods should map to the following actions:

| Action        | Scope         | Method        | Result
| --------------|---------------|---------------|-----------------------------------------------
| Read          | Collection    | `GET`         | Lists a collection of entities
| Read          | Entity        | `GET`         | Returns a single entity
| Create        | Collection    | `POST`        | Adds a new entity to a collection
| Update        | Entity        | `PUT`         | Replace an entity with a new instance
| Update        | Entity        | `PATCH`       | Update individual properties of an entity
| Delete        | Entity        | `DELETE`      | Delete an instance of an entity

> *Note:* Ideally, each entity and collection should support the above actions, although not all users will be authorized to execute these actions.

### URL Conventions

> *Important:* The URL path should be used as the primary means of representing entities (e.g., `/Borges`) and collections of entities (e.g., `/Authors`). Avoid using the URL for other concepts.

- URLs should be logically organized by URL path, with each "folder" representing a collection of entities (e.g., `/Authors`), an entity key (e.g., `/Borges`), an attribute (e.g., `/DateBorn`), or, if necessary, an action (e.g., `/Checkout`)
  - If an action cannot be intuitively expressed using an entity / method pairing, the URL may be extended to represent actions (e.g., `/Checkout`)
  - Generally, each URL should resolve to a distinct entity or entity collection; URLs should avoid representing state (including queries) or actions

> *Note:* An exception to this is well-established types (or enums) which can be used to partition a collection into *distinct* sets; e.g., `/Books/Available/`, `/Books/CheckedOut/`, `/Books/Lost/`.

- Where technically feasible, entities and relationships should support dynamic composition to allow multiple logical entry points

> For instance, `/Authors/Borges/Books/Ficciones/DatePublished/` and `/Users/Jeremy/Favorites/Books/Ficciones/DatePublished` should represent the same object.

- Generally, public entity names (e.g., `/Books`) should map to server-side class names (e.g., `BookCollection`) and SQL table names (`catalog_Books`)
  - E.g., Outside of established conventions (e.g., the `Collection` suffix, the `catalog_` namespace prefix), entity names should be consistently applied
  - Developers should be able to quickly and intuitively understand the relationship between a web service, class library, and data structure
- Consider using key/value pairs to support composite primary keys (e.g., `/Articles(ArticleID=5,Locale='en-US')`, as per OData conventions)

### Query String Conventions

> *Important:* The query string should be used as the primary means of querying collections (e.g., filtering, sorting, paging)

- All entity collections should support, at minimum, filtering, sorting, and paging
  - Querying capabilities should not be applied inconsistently based on immediately foreseeable needs
- Querying capabilities should be represented by a consistent vocabulary (e.g., `$filter`, `$orderby`, `$skip`, `$top`, as per OData conventions)
- Query string parameters should *not* be used for setting actions (e.g., `?Action=Add`) or content (e.g., `?Name=Borges`); instead, use the HTTP method and HTTP body
- The query string should provide an alternative means of defining HTTP Headers (e.g., `?$format=json`, as per OData conventions)

### Body Conventions
- The body should be used for delivering actual *content*, both when reading (i.e., the response body) and writing (i.e., the request body)
- The body should be formatted using a well-established data format, such as JSON or XML
  - If practical, the body should be formatted with a well-established schema (e.g., ``)
- If multiple data formats are available, the client should be able to specify the requested format using either the `Accepts` header
  - Ideally, the client should also be able to define the content type using an optional query string parameter (e.g., `?$format=json`, as per OData conventions)
  - The preferred default should always be JSON, when available
- Consider providing a list of actions associated with the entity in the response body (as per [Hypermedia as the Engine of Application State (HATEOAS)](https://en.wikipedia.org/wiki/HATEOAS) constraints)
  - Ideally, this will reflect the current state of the entity as well as the authorization of the currently authenticated user
  - In XML, the preferred format is a `link` element with a `rel` and `href` attribute (as per [ATOM Standard](https://en.wikipedia.org/wiki/Atom_(standard)))
  - In OData, the preferred format is to use OData metadata annotations (e.g., `@odata.editLink`)

<!--

## Language Features


### Authentication


## Comments


### Documentation


## Acknowledgments

-->