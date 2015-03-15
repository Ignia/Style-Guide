# C-Based Languages

While C#, Java, and JavaScript are very different languages, they do share one thing in common: C-based syntax. For this reason, many style preferences can be applied to each. Indeed, since developers may be switching back and forth among these languages, maintaining consistency between each is not only important for readability but also developer productivity.

## Identifiers
- Class, type and enum names should use `PascalCase` (e.g., `ClassName`)
- Private properties (or fields) should begin with a single underscore (e.g., `this._privateProperty`)
- Local variables and parameters should use `camelCase` (e.g., `localVariable`)
- Constants should use `UPPER_CASE` separated by underscores (e.g., `SOME_CONSTANT`)
- Identifiers should *not* contain underscores (except as noted above), hyphens, or numbers
- Identifiers should *not* use [Hungarian notation](https://msdn.microsoft.com/en-us/library/aa260976%28v=vs.60%29.aspx) (i.e., 1-3 character type prefixes)
- Define one class per file; the filename should be the same as the class name (including casing)
- Boolean identifiers should begin with a present indicative (e.g., `is`, `has`, etc.)
- If only one object instance is expected to exist in scope, and the class name describes its purpose, the instance variable may be named after the class (except in `camelCase`)

> *Note:* C# and JavaScript vary in casing requirements for class members (such as properties and methods) and namespaces; in C# they use `PascalCase`; in JavaScript they use `camelCase`.

## Variables
- Constants and configuration variables should be placed at the top of the file, and clearly identified via a comment
- Variables in constructors should have defaults assigned (e.g., using ?? syntax in C# or || in JavaScript)

## Spacing
- Place one space before opening braces
- Pad all operators (e.g., `=`, `+`, `\`) with spaces (e.g., 'x = y * 2')
- Place spaces *outside* of parentheses, but not immediately inside
- Do not pad arguments to function calls or control flow expressions

## Formatting
- Object literal syntax should place one property per line, indented two spaces
- Array literal syntax may *optionally* place multiple values on one line (e.g., `[1, 2, 3, 4]`)
- Opening braces (i.e., `{`) should be on the same line as the preceding identifier or expression
- Closing braces (i.e., `}`) should be on a new line, not indented with the logic they enclose
- Always use braces with multi-line blocks (may skip for single-line, single-statement expressions)
- `if` and `else` should always be on the same column; same with `try`, `catch`, `finally`
  - i.e., do not place `else`, `catch`, or `finally` on the same line as the previous closing brace (`}`)
- Do not use leading commas; commas should always appear *after* their preceding statement
- Any `;` used as a statement terminator must be at the end of the line (i.e., only one statement per line)
- The `?` and `:` in a ternary conditional must have space on *both* sides

> *Note:* Prior to 2015, Ignia used the [Banner Indent Style](http://en.wikipedia.org/wiki/Indent_style#Banner_style), which uses an indented trailing brace. Any legacy code being used should be updated to the above standards in bulk before implementation.

<!-- http://en.wikipedia.org/wiki/Indent_style#Variant:_Stroustrup -->

### Line Wrapping
- If *any* elements must be placed on a new line, consider moving *all* elements to new lines for consistency
- Follow standard indentation rules; subsequent lines should not be indented more than two spaces (e.g., to align with a `(`, for instance)
- Function arguments should be on the same line as the function
  - If this is not possible, function arguments should each be placed on their own line and indented two spaces
- If expressions must be placed on multiple lines, each new line should begin with the operator (e.g., `+`) and be indented two spaces
- If method chains must be placed on multiple lines, each new line should begin with the period (i.e., `.`) and be indented two spaces

## Comments
- Use documentation-style comments as permitted by each language (e.g., XmlDoc in C#)
- Use `/* ... */` syntax for multi-line comments *unless required otherwise by documentation format*

> *Note:* Prior to 2015, Ignia used flower-boxes for comments. These should be replaced with documentation-style comments when updating legacy code.

## Syntax
- Always assign variables at the top of their scope; assignments can come later, if needed
- Avoid excessive nesting; if a method requires more than three layers of nesting, consider refactoring
  - Effective use of return, break, continue, and exceptions can help prevent excessive nesting
- Do not use an `else` statement after a `return`; it is unnecessary




