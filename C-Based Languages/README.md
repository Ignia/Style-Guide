# C-Based Languages

While C#, Java, and JavaScript are very different languages, they do share one thing in common: C-based syntax. For this reason, many style preferences can be applied to both. Indeed, since developers may be switching back and forth between these languages, maintaining consistency between each is not only important for readability but also developer productivity.

## Spacing

## Formatting
- Object initializers should place one property per line, indented two spaces
- Array initializers may *optionally* place multiple values on one line (e.g., `[1, 2, 3, 4]`)
- Open braces (i.e., `{`) should be on the same line as the preceding identifier or expression
- Close braces (i.e., `}`) should be on a new line, not indented with the logic they enclose

> *Note:* Prior to 2015, Ignia used the [Banner Indent Style](http://en.wikipedia.org/wiki/Indent_style#Banner_style), which uses an indented trailing brace. Any legacy code being used should be updated to the above standards in bulk before implementation.

http://en.wikipedia.org/wiki/Indent_style#Variant:_Stroustrup

### Line Wrapping
- Function arguments should be on the same line as the function
  - If this is not possible, function arguments should each be placed on their own line and indented two spaces
- If expressions must be placed on multiple lines, each new line should begin with the operator (e.g., `+`) and be indented two spaces

## Identifiers
- Class, type and enum names should use PascalCase (e.g., `ClassName`)
- Private properties (or fields) should begin with a single underscore (e.g., `this._privateProperty`)
- Local variables should use camelCase (e.g., `localVariable`)
- Constants should use UPPER_CASE separated by underscores (e.g., `SOME_CONSTANT`)
- Identifiers should *not* contain underscores (except as noted above), hyphens, or letters

## Comments
- Use documentation style comments as permitted by each language

> *Note:* Prior to 2015, Ignia used flower-boxes for comments. These should be replaced with documentation-style comments when updating legacy code.

## Syntax


