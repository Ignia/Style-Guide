# ASP.NET

While ASP.NET applications typically use C# and HTML, they also introduce their own syntax and coding conventions, which are dependent on the specific technology and templating engine used.

> *Note:* This style guide inherits rules from the [C# Style Guide](../C-Based%20Languages/C%23/), [C-Based Languages Style Guide](../C-Based%20Languages/), [SGML-Based Languages](../SGML-Based%20Languages/), [HTML5](../SGML-Based%20Languages/HTML5.md), and the [Global Style Guide](../README.md). This document will supersede our legacy [User Controls Style Guide](../Legacy/User.Controls.doc).

> # Placeholder Content
> This page is a placeholder; additional content will be provided at a later date.

## Contents
- [Language Features](#language-features)
  - [Caching](#caching)
  - [ASP.NET Web Forms](#aspnet-web-forms)

<!--
## Contents
- [Identifiers](#identifiers)
- [Spacing](#spacing)
- [Formatting](#formatting)
- [Acknowledgments](#acknowledgments)

## Spacing

## Formatting
-->

## Language Features
- Use (or extend) the ASP.NET Identity libraries for authentication (including single-sign-on), roles-based authorization, and, where practical, profile management
  - If a custom database is necessary, it is preferred to write providers for the ASP.NET Identity libraries than to create a completely novel system

### Caching
- If the contents of a page are not dynamic, or vary based on limited parameters, consider using `OutputCache` to improve performance
- `OutputCache` should always use the `CacheProfile` unless the parameters are truly page specific
- Pages that are rarely accessed should not use output caching as it increases memory requirements
- For pages that vary by state variables (e.g., cookies, session, user profile properties, etc) use `VaryByCustom`

### ASP.NET Web Forms
- If page-specific code is required, it should be placed in a `CodeFile`; this is preferred to `CodeBehind`, which requires pre-compilation into a centralized assembly
  - The name of the `CodeFile` should be the same as the page, plus `.cs`; e.g., a `Home.aspx` page will have a `CodeFile` set to `Home.aspx.cs`
  - Typically, page-specific code should be minimal, instead relying on centralized class libraries; this should act similar to a controller in an MVC application
- Make use of User Controls to parameterize and centralize repetitive elements, especially across pages
- Prefer use of the `ListView` to other repeaters; it provides complete control over markup, while also offering more convenience-features than `Repeater`
- Consider creating custom `DataSourceControl` classes as part of a data access layer to simplifying querying and binding to the interface
