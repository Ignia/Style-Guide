# C# Style Guide

While most of Ignia's front-end code is written exclusively in HTML5 (without any server preprocessing), we predominantly rely on C# for service layers (e.g., exposing REST APIs). Much of our C# guidelines inherit from our general [C-Based Languages](../README.md) guidelines, although there are some specific considerations unique to C#.

## Style Guides
- [Class Libraries](../C%23/Class%20Libraries.md)

> *Note:* This style guide inherits rules from the [C-Based Languages Style Guide](../README.md) and the [Global Style Guide](../../README.md). This document supersedes our legacy [C# Style Guide](../Legacy/C%23.StyleGuide.doc) (Microsoft Word).

## Contents
- [Identifiers](#identifiers)
- [Formatting](#formatting)
- [Comments](#comments)
  - [XML Documentation](#xml-documentation)
- [Language Features](#language-features)

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