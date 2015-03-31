# C# Style Guide

While most of Ignia's front-end code is written exclusively in HTML5 (without any server preprocessing), we predominantly rely on C# for service layers (e.g., exposing REST APIs). Much of our C# guidelines inherit from our general [C-Based Languages](../README.md) guidelines, although there are some specific considerations unique to C#.

## Style Guides
- [Class Libraries](../C%23/Class%20Libraries.md)

> *Note:* This style guide inherits rules from the [C-Based Languages Style Guide](../README.md) and the [Global Style Guide](../../README.md)

## Contents
- [Identifiers](#identifiers)
- [Formatting](#formatting)
- [Comments](#comments)
  - [XML Documentation](#xml-documentation)
- [Language Features](#language-features)
  - [ASP.NET](#aspnet)
    - [Caching](#caching)
    - [ASP.NET Web Forms](#aspnet-web-forms)

<!--
  - [Acknowledgments](#acknowledgments)
  -->

## Identifiers
- Class members (e.g., properties, functions) and namespaces should be `PascalCase` (e.g., `DoSomething()`)

## Formatting
- The `namespace` may be introduced above a file header; this allows the file header to document the `class`, not the `namespace` (which is usually not unique to the file)
- Each attribute should be placed on its own line

## Language Features
- Any `using` directives should be placed inside the `namespace`, not outside of it
- Local variables *should* use type inference (i.e., the `var` keyword for declaring variables)
- Prefer default arguments to overloading unless default arguments will cause unintuitive combinations of parameters
- When repeatedly using a regular expression (e.g., on a frequently requested page or within a loop), make use of the [`RegexOptions.Compiled` flag](https://msdn.microsoft.com/en-us/library/system.text.regularexpressions.regexoptions(v=vs.110).aspx)

### ASP.NET
- Use (or extend) the ASP.NET Identity libraries for authentication (including single-sign-on), roles-based authorization, and, where practical, profile management
  - If a custom database is necessary, it is preferred to write providers for the ASP.NET Identity libraries than to create a completely novel system

#### Caching
- If the contents of a page are not dynamic, or vary based on limited parameters, consider using `OutputCache` to improve performance
- `OutputCache` should always use the `CacheProfile` unless the parameters are truly page specific
- Pages that are rarely accessed should not use output caching as it increases memory requirements
- For pages that vary by state variables (e.g., cookies, session, user profile properties, etc) use `VaryByCustom`

#### ASP.NET Web Forms
- If page-specific code is required, it should be placed in a `CodeFile`; this is preferred to `CodeBehind`, which requires pre-compilation into a centralized assembly
  - The name of the `CodeFile` should be the same as the page, plus `.cs`; e.g., a `Home.aspx` page will have a `CodeFile` set to `Home.aspx.cs`
  - Typically, page-specific code should be minimal, instead relying on centralized class libraries; this should act similar to a controller in an MVC application
- Make use of User Controls to parameterize and centralize repetitive elements, especially across pages
- Prefer use of the `ListView` to other repeaters; it provides complete control over markup, while also offering more convenience-features than `Repeater`
- Consider creating custom `DataSourceControl` classes as part of a data access layer to simplifying querying and binding to the interface

## Comments

### XML Documentation
- Classes and class members should be documented using Microsoft's [XML Documentation Features](https://msdn.microsoft.com/en-us/library/z04awywx.aspx)
- XML elements within comments should follow Ignia's [SGML formatting rules](../../SGML-Based%20Languages/README.md)
- XML documentation should use the multi-line comment format with each line prefixed with two spaces and and asterisk
- The closing comment tag should be on its own line and indented two spaces
- XML comments should be indented one space from the preceding asterisk, thus starting at column 5 (four spaces from the start of the line)
- The first element (typically the `summary` element) should begin on the same line as the opening comment (i.e., `/** <summary>`)
- If the documentation requires more than one line, it should start on a new line, and be indented two spaces from the parent XML element (i.e., three spaces from the preceding asterisk)
- All members should define `summary`; members should define `returns` if they are not `void`; methods should define `param`; `remarks` is optional, but encouraged, particularly for classes

```c#
/** <summary>
  *   Adds an instance of Book to the Books collection.
  * </summary>
  * <remarks>
  *   Adding a Book object to the Books collection does not automatically save the instance of the Book to the
  *   database. To save the update, call <see cref="Save()" />.
  * </remarks>
  * <param name="book">The reference to the instance of the Book to be added to the Books collection.</param>
  * <returns>Returns a reference to <paramref name="book" />.</returns>
  */
```
<!--
## Acknowledgments
-->