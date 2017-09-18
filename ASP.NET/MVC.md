# ASP.NET MVC

While MVC  applications typically use C# and HTML, they also introduce their own syntax and coding conventions, which are dependent on the specific technology and templating engine used.

> *Note:* This style guide inherits rules from the [C# Style Guide](../C-Based%20Languages/C%23/), [C-Based Languages Style Guide](../C-Based%20Languages/), [SGML-Based Languages](../SGML-Based%20Languages/), [HTML5](../SGML-Based%20Languages/HTML5.md), and the [Global Style Guide](../README.md).

> # Placeholder Content
> This page is a placeholder; additional content will be provided at a later date.

## Contents
- [General](#general)
- [Organization](#organization)
- [Language Features](#language-features)
  - [Caching](#caching)

<!--
## Contents
- [Identifiers](#identifiers)
- [Spacing](#spacing)
- [Formatting](#formatting)
- [Acknowledgments](#acknowledgments)

## Spacing

## Formatting
-->

## General
- Use Dependency Injection
  - Use site-specific `ControllerFactory` (e.g., `/ControllerFactory.cs`) as _composition root_
  - Consider using an Inversion of Control (IoC) container for finding controllers by conventions
    - For sites with few controllers, manually establishing dependencies is preferred

## Organization
- Use out-of-the-box conventions for file locations
  - Store controllers in `/Controllers` folder
  - Store views in `/Views` folder
- Only store site-specific view models in `/Models`
  - All other models should be e.g. entity objects in separate assembly
- Break site layout into multiple partial views
  - Establish `LayoutController` for managing partial views
  - Consider a `/Layout/` folder with `_Layout.cshtml`, `Menu.cshtml`, `Footer.cshtml`, etc.
  - Consider treating each view as a "component" in the [SASS structure](https://github.com/Ignia/Sass-Structure)

## Language Features

### Models
- Strongly type views when practical
- Prefer specialized view models for reusable partial views
  - This allows partial views to be parameterized
  - This also helps standardize the model despite disparate parent views

### Views
- Prefer Razor parsing engine for views
- Consider explicitly defining `@{ Layout }` property for clarity
- Prefer using `@helper` or `@functions` over multiline inline code blocks
  - Prefer helpers for code responsible for outputting markup
  - Follow Ignia's [C# Style Guide](../C-Based%20Languages/C%23/) for these

### Controllers
- Each Controller should use _constructor injection_
  - This will include e.g. data repositories (say, `IUserRepository`, `IPostRepository`)

### Authentication
- Use (or extend) the ASP.NET Identity libraries for authentication (including single-sign-on), roles-based authorization, and, where practical, profile management
  - If a custom database is necessary, it is preferred to write providers for the ASP.NET Identity libraries than to create a completely novel system

### Caching
- If the contents of a page are not dynamic, or vary based on limited parameters, consider using `OutputCache` to improve performance

<!--
- `OutputCache` should always use the `CacheProfile` unless the parameters are truly page specific
- Pages that are rarely accessed should not use output caching as it increases memory requirements
- For pages that vary by state variables (e.g., cookies, session, user profile properties, etc) use `VaryByCustom`
-->
