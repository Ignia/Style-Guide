# Ignia Style Guide
Ignia's internal style guide for languages and formats we work in most frequently.

## Motivation
Code may need to be executed by computers, but it also needs to be maintained by humans. For this reason, Ignia places high value on code that is readable, uniformly formatted, and consistent with emerging conventions. Ignia has not only maintained rigid coding standards since our inception in 1998, but continues to evolve them to keep pace with both technology and market trends.

## Style Guides
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

## Contents
- [General Principles](#general-principles)
- [Identifiers](#identifiers)
- [Variables](#variables)
- [Spacing](#spacing)
- [Comments](#comments)
- [Encoding](#encoding)
- [No Opinion](#no-opinion)

## General Principles
- Be consistent
- Do not be afraid of whitespace; it greatly enhances readability
- Leverage well-established conventions; break with convention only with good rationale
- When working with existing code bases, always follow any established conventions (i.e., ignore this document)

## Identifiers
- Avoid arbitrary abbreviations in identifiers (e.g., variables, class names, etc.)
- Only use abbreviations that are well-established and widely understood (e.g., ID, XML, HTML)
- When abbreviations are used, they should follow the casing standards (e.g., `Html` in `PascalCase`, not `HTML`)
  - An exception is granted for two letter acronyms (e.g., `ID`, `IO` in `PascalCase`) ([source](https://msdn.microsoft.com/en-us/library/ms229043(v=vs.110).aspx))
- Use consistent casing for identifiers of each type (e.g., all variables should be `camelCase`)
- Do not use identifiers that conflict with keywords in commonly used programming languages ([source](https://msdn.microsoft.com/en-us/library/ms229045(v=vs.110).aspx))

## Spacing
- Use soft tabs set to two spaces
- Use tab stops set to eight spaces
- Place empty lines to create visual groupings between related code
- Consecutive variable assignments should have their values set at line 33 (indented 32 characters)
- Lines should be no longer than 96 characters, and must not exceed 128
- End files with a single newline character

## Comments
- Comments are always preceded by a blank line
- Comments start with a capital letter; full sentences end with a period.
- There must be a single space between the comment token and the comment text
- Author notes should be prefixed with `### {ABCD} {EFG}{012349}: ` where:
  - `ABCD` is `NOTE`, `TODO`, or `HACK`
  - `{EFG}` is the author's initials (e.g., `JJC`)
  - `012349` is the date in the format DDMMYY (e.g., `031315`)
  - E.g., `### TODO JJC031315: Fix Internet Explorer 9 compatibility issue with CSS3 selectors.`

## Encoding
- Use UTF-8 encoding

## No Opinion
- Unix-style carriage returns (i.e., `\n`) v. Windows-style (`\r\n`)


<!--
## Acknowledgments
-->
