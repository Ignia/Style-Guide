# Ignia Style Guide
Ignia's internal style guide for languages and formats we work in most frequently.

## Motivation
Code may need to be executed by computers, but it also needs to be maintained by humans. For this reason, Ignia places high value on code that is readable, uniformly formatted, and consistent with emerging conventions. For this reason, Ignia has not only maintained rigid coding standards since our inception in 1998, but continued to evolve them to keep pace with technology, as well as market trends.

## Styles
- [Common Rules](#common-rules) (see below)
- [C-Based Languages](./C-Based%20Languages/)
  - [JavaScript](./C-Based%20Languages/JavaScript)
    - [TypeScript](./C-Based%20Languages/JavaScript/TypeScript.md)
    - [JSON](./C-Based%20Languages/JavaScript/JSON.md)
  - [C#](./C-Based%20Languages/C%23)
    - [Class Libraries](./C-Based%20Languages/C%23/Class%20Libraries.md)
- [CSS-Based Languages](./CSS-Based%20Languages/)
  - [Sass](./CSS-Based%20Languages/Sass.md)
- [SGML-Based Languages](./SGML-Based%20Languages/)
  - [HTML5](./SGML-Based%20Languages/HTML5.md)

## Common Rules

### Spacing
- Use soft tabs set to two spaces
- Use tab stops set to eight spaces
- Place empty lines to create visual groupings between related code
- Consecutive variable assignments should have their values set at line 33 (indented 32 characters)
- Lines should be no longer than 96 characters, and must not exceed 128

### Comments
- Comments are always preceded by a blank line
- Comments start with a capital letter; full sentences end with a period.
- There must be a single space between the comment token and the comment text

### Identifiers
- Avoid arbitrary abbreviations in identifiers (e.g., variables, class names, etc.)
- Only use abbreviations that are well-established and understood (e.g., ID, XML, HTML)
- When abbreviations are used, they should be follow the casing standards (e.g., Html in PascalCase)
- Use consistent casing for identifiers of each type (e.g., all variables should be camelCase)

<!--
## Acknowledgments
-->