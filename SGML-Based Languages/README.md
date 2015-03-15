# SGML-Based Languages

SGML is, loosely speaking, the parent language of HTML and XML. While HTML5 technically broke away from SGML compliance it nonetheless provides the best umbrella term for styles related to these two technologies.

## Style Guides
- [HTML5](./HTML5.md)

> *Note:* This style guide inherits rules from the [Global Style Guide](../README.md)

## Contents
- [Spacing](#spacing)
- [Formatting](#formatting)
- [Comments](#comments)
- [Capitalization](#capitalization)

## Spacing
- Child elements should always be nested *exactly* two spaces from their parent (this includes `<body>` and `<head>` in relation to `<html>`)

## Formatting
- Always use double-quotes (not single-quotes) for attribute values
- All attribute values should be quoted (even if considered optional)
- Always place elements on their own line *unless* no child has more than one direct child
- Avoid encoding markup in other languages (e.g., C#, JavaScript) when possible; instead, use a data-binding library

```html
<!-- bad -->
<ul><li>Item 1</li><li>Item 2</li></ul>

<!-- good -->
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<!-- fine -->
<a href="#"><span class="thumbnail"><img src="#" alt="#" /></span></a>
```

## Comments
- If a block of markup includes a starting comment (e.g., `<-- Header -->`) and is more than five lines of code, include a closing comment (e.g., `<-- /Header -->`)

## Capitalization
- All element and attribute names should be lowercase (when considered optional)

> **Exception:** ASP.NET provides declarative syntax for server-side controls, some of which overlap with HTML elements. In this case, ASP.NET-specific properties should use PascalCase to distinguish them from client-side properties.

