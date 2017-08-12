# Ignia OnTopic

While Ignoa Ontopic applications typically use C#, HTML, and MVC, they also introduce their own organizational, syntax, and coding conventions.

> *Note:* This style guide inherits rules from the [C# Style Guide](../C-Based%20Languages/C%23/), [C-Based Languages Style Guide](../C-Based%20Languages/), [SGML-Based Languages](../SGML-Based%20Languages/), [HTML5](../SGML-Based%20Languages/HTML5.md), [MVC](../ASP.NET/MVC.md), and the [Global Style Guide](../README.md).

> # Placeholder Content
> This page is a placeholder; additional content will be provided at a later date.

## Contents
- [General](#general)
- [Content Types](#content-types)
- [Templates](#templates)

<!--
## Contents
- [Identifiers](#identifiers)
- [Spacing](#spacing)
- [Formatting](#formatting)
- [Language Features](#language-features)
- [Acknowledgments](#acknowledgments)

## Spacing

## Formatting
-->

## General
- Prefer [MVC](../ASP.NET/MVC.md) over legacy [Web Forms](../ASP.NET/) implementation

## Content Types
- Store commonly used attributes in `Configuration:ContentTypes:Attributes` for centralization
  - These can be referenced on individual Content Types using Topic Pointers (i.e., `DerivedTopic`)
  - When deriving attributes, do not override the `Key` attribute; this facilitates polymorphism and duck-typing
- Rely on content type inheritance (via nesting) to centralize common attribute patterns
  - E.g., All content types that will be used as web pages should be placed under `Page`
- Provide strongly-typed topics (derived from `Topic`) to expose strongly-typed properties or complex business logic
- Prefer content types based on business entities (e.g., FAQ) over presentation (e.g., Accordion)
  - Consider using presentation-oriented content types, however, to centralize common patterns
- Consider inherited content types for providing friendlier labels

## Templates
- Rely on the out-of-the-box views functionality to provide different templates for the same data model
  - Views should be follow the convention `/Views/ContentType/ViewName.cshtml` (e.g., `/Views/ContentList/Accordion.cshtml`)
  - For a default view to be used independent of content type, follow the convention `/Views/ViewName.cshtml` (e.g., `/Views/JSON.cshtml`)
- Use includes (e.g., `@Html.Partial("~/Views/ContentList/Accordion.cshtml")') to centralize presentation with common data models

<!--
## Language Features
-->
