# Ignia Style Guide
Ignia's internal style guide for languages and formats we work in most frequently. For brevity, this style guide focuses more on guidelines and less on the reasons.

## Motivation
Code needs to be executed by computers, but it also needs to be maintained by humans. For this reason, Ignia places high value on code that is readable, uniformly formatted, and consistent with emerging conventions. This is especially important since Ignia works with a diverse set of clients, partners, and contractors. Ignia has not only [maintained rigid coding standards since our inception in 1998](./Legacy/), but continues to evolve them to keep pace with both technology and market trends.

## Style Guides
- [Common Rules](#contents) (see below)
- [C-Based Languages](./C-Based%20Languages/)
  - [JavaScript](./C-Based%20Languages/JavaScript)
    - [Angular](./C-Based%20Languages/JavaScript/Angular.md)
    - [ECMAScript 6](./C-Based%20Languages/JavaScript/ECMAScript%206.md)
    - [JSON](./C-Based%20Languages/JavaScript/JSON.md) (and JavaScript object literal notation)
  - [C#](./C-Based%20Languages/C%23)
    - [Class Libraries](./C-Based%20Languages/C%23/Class%20Libraries.md)
- [CSS-Based Languages](./CSS-Based%20Languages/)
  - [Sass](./CSS-Based%20Languages/Sass.md)
- [Media Files](./Media%20Files/)
- [REST APIs](./REST%20APIs/)
- [SGML-Based Languages](./SGML-Based%20Languages/)
  - [HTML5](./SGML-Based%20Languages/HTML5.md)
- [SQL-Based Languages](./SQL-Based%20Languages/)
- [Legacy Style Guides](./Legacy/)

<!-- [TypeScript](./C-Based%20Languages/JavaScript/TypeScript.md) -->

## Contents
- [General Principles](#general-principles)
- [Identifiers](#identifiers)
- [Variables](#variables)
- [Spacing](#spacing)
- [Comments](#comments)
- [Encoding](#encoding)
- [No Opinion](#no-opinion)

## General Principles
- Do not be afraid of whitespace; it greatly enhances readability
- Leverage well-established conventions; break with convention only with good rationale
- When working with existing code bases, always follow any established conventions (i.e., ignore this document)
- ***Be consistent!***

## Identifiers
- Identifiers should be descriptive (e.g., `userProfile` not `u`)
- Avoid arbitrary abbreviations in identifiers (e.g., in variable names, class names, etc.)
- Only use abbreviations that are well-established and widely understood (e.g., ID, XML, HTML)
- When abbreviations are used, they should follow the casing standards (e.g., `Html` in `PascalCase`, not `HTML`)
  - An exception is granted for two-letter acronyms (e.g., `ID`, `IO` in `PascalCase`) ([source](https://msdn.microsoft.com/en-us/library/ms229043(v=vs.110).aspx))
- Use consistent casing for identifiers of each type (e.g., all variables should be `camelCase`)
- Do not use identifiers that conflict with keywords in commonly used programming languages ([source](https://msdn.microsoft.com/en-us/library/ms229045(v=vs.110).aspx))

## Spacing
- Use soft tabs set to two spaces
- Use tab stops set to eight spaces, when supported
- Use rulers set to every thirty-two characters (e.g., 32, 64, 96...), when supported
- Consecutive variable or property assignments should have their values set at line 33 (i.e., the 32 character ruler), e.g.,
```css
body {
  background-color:             : rgba(255, 255, 255, 1);
  font-family:                  : 'Helvetica',                  // Optional multi-line format
                                  'Arial',
                                  sans-serif;
  font-size:                    : 12px;
  font-size:                    : 1.2rem;
  line-height:                  : 14px;
  line-height:                  : 1.3rem;
}
```
- Lines should be no longer than 96 characters, and must not exceed 128 (including indentation)
- Insert empty lines to create visual groupings among related code blocks
- End files with a single newline character; this aids with diffs in source control

## Comments
- Comments are always preceded by a blank line, unless they are on the same line as code
- When using multi-line comments, there must be a single space between the comment token and the comment text
- Comments start with a capital letter; full sentences end with a period
- Author notes should be prefixed with `### {ABCD} {EFG}{012349}: ` where:
  - `ABCD` is `NOTE`, `TODO`, `HACK`, `EDIT`, or `REM`
  - `{EFG}` is the author's initials (e.g., `JJC`)
  - `012349` is the date in the format `DDMMYY` (e.g., `031315`)
```js
//### TODO JJC031315: Fix Internet Explorer 9 compatibility issue with CSS3 selectors.
```

## Encoding
- Use UTF-8 encoding

## No Opinion
- Unix-style carriage returns (i.e., `\n`) v. Windows-style (`\r\n`)

## Feedback
If you find errors in this guide, or feel we should reevaluate a particular standard, feel free to [open an issue](https://github.com/Ignia/Style-Guide/issues). We welcome feedback.

<!--
## Acknowledgments
-->
