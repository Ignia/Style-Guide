# C-Based Languages

While C#, Java, and JavaScript are very different languages, they do share one thing in common: C-based syntax. For this reason, many style preferences can be shared across them. Indeed, since developers may be switching back and forth among these languages, maintaining consistency between each is not only important for readability but also developer productivity.

## Style Guides
- [JavaScript](./JavaScript)
  - [Angular](./JavaScript/Angular.md)
  - [ECMAScript 6](./JavaScript/ECMAScript%206.md)
  - [JSON](./JavaScript/JSON.md)
<!-- [TypeScript](./JavaScript/TypeScript.md) -->
- [C#](./C%23)
  - [Class Libraries](./C%23/Class%20Libraries.md)

> *Note:* This style guide inherits rules from the [Global Style Guide](../README.md).

## Contents
- [Identifiers](#identifiers)
  - [Capitalization](#capitalization)
  - [Naming Conventions](#naming-conventions)
- [Variables](#variables)
- [Spacing](#spacing)
- [Syntax](#syntax)
- [Formatting](#formatting)
  - [Line Wrapping](#line-wrapping)
- [Comments](#comments)
- [Language Features](#language-features)
- [Acknowledgments](#acknowledgments)

## Identifiers

### Capitalization
| Type                          | Case                          | Example
| ------------------------------|-------------------------------|-------------------------------
| Class                         | `PascalCase`                  | `ShoppingCart`
| Enum                          | `PascalCase`                  | `CheckoutStatus`
| Private Properties            | `_camelCase`                  | `_shoppingCart`
| Local Variables               | `camelCase`                   | `shoppingCart`
| Parameters                    | `camelCase`                   | `checkoutStatus`
| Constants                     | `UPPER_SNAKE_CASE`            | `IMAGES_DIRECTORY`

> *Note:* [C#](./C%23/README.md) and [JavaScript](./JavaScript/README.md) vary in casing requirements for class members (such as properties and methods) and namespaces; in C# they use `PascalCase`; in JavaScript they use `camelCase`.

### Naming Conventions
- Identifiers should *not* contain underscores (except as noted above), hyphens, or numbers
- Identifiers should *not* use [Hungarian notation](https://msdn.microsoft.com/en-us/library/aa260976%28v=vs.60%29.aspx) (i.e., `strName`, `btnPassword`)
- Boolean identifiers should begin with a present indicative (e.g., `isVisible`, `hasReplies`, etc.)
- Classes, namespaces, and non-Boolean properties should use nouns (e.g., `Author`, `Connection`)
- Methods and events should use verbs (e.g., `addAuthor()`, `connect()`)
- Events should use present tense (e.g., `loading`) or past tense (e.g., `loaded`) to indicate before and after states
- Identifiers representing collections (e.g., arrays) should be pluralized (e.g., `author.books`)
- If a reference property has no additional contextual meaning beyond that of its type, give it the name of the type (e.g., `book.author` to represent an `Author` type)
  - If there *is* a clear contextual meaning beyond the type name, reflect that in the name (e.g., `book.editor` or `book.primaryAuthor` instead of `book.author`)
- If only one object instance is expected to exist in scope, and the type name describes its purpose, the instance variable may be named after the type (e.g., using `databaseConnection` to represent the type `DatabaseConnection`)
- Define one class per file; the filename should be the same as the class name, including casing (e.g., an `Author` class should be in an `Author.js` file)

> **Important**: Do not invent new identifiers arbitrarily; `Author`, `book.Author`, `_author`, `author`, and `addAuthor()` all represent the same object type.

<!-- Can these be distributed to other sections? -->
## Variables
- Constants and configuration variables should be placed at the top of the file, and clearly identified via a comment
- Variables initialized in constructors should have defaults assigned (e.g., using `??` syntax in C# or `||` in JavaScript)

## Spacing
- Place one space before opening braces (e.g., never have `if{...}`)
- Pad all operators (e.g., `=`, `+`, `\`) with spaces (e.g., 'x = y * 2', not `x=y*2`)
- Place spaces *outside* of parentheses, but not immediately inside (e.g., `if (isCurrent)` not `if( isCurrent )`)
- Do not place spaces outside parenthesis for method calls or brackets for indexers

```js
var totalSales = 0;
for (i = 0; i < author.books.length; i++) {
  totalSales = totalSales + author.books[i].sales;
}
```

## Syntax
- Always assign variables at the top of their scope; assignments can come later, if needed
- Define class or prototype members by order of: constructors, properties, methods, events
- Avoid excessive nesting; if a method requires more than three layers of nesting, consider refactoring
  - Effective use of return, break, continue, and exceptions can help prevent excessive nesting
- Do not use an `else` statement after a `return`; it is unnecessary

## Formatting
- Opening braces (i.e., `{`) should be on the same line as the preceding identifier or expression
- Closing braces (i.e., `}`) should be on a new line, not indented with the logic they enclose
- Object literal syntax should place one property per line, indented two spaces
- Array literal syntax may *optionally* place multiple values on one line (e.g., `[1, 2, 3, 4]`)

```js
var author {
  name                          : 'Jorge Luis Borges',
  books                         : ['Ficciones', 'Labyrinths', 'El Aleph', 'Poesía completa'],
  born                          : '1899-08-24',
  died                          : '1986-06-14'
}
```

- Always use braces with multi-line blocks (may skip for single-line, single-statement expressions; e.g., `if (!author) return`)
- `if`, `else`, `try`, `catch`, and `finally` should always be on the same column
  - i.e., do not place `else`, `catch`, or `finally` on the same line as the previous closing brace (`}`)
- Any `;` used as a statement terminator must be at the end of the line (i.e., only one statement per line)
  - The one exception is annotation-style comments which may appear after the `;`
- The `?` and `:` in a ternary conditional must have space on *both* sides

```js
let author;                     // Reference to the author object
let isFavorite;                 // Is the author a "favorite" of the current user?

function addAuthor(author) {

//Ignore if author was not passed
  if (!author) return;

//Check to see if author exists
  if (authors[author.name]) {
    Object.getOwnPropertyNames(author).forEach(
      function(val, idx, array) {
        authors[author.name][val] = author[val];
      }
    );
  }

//Otherwise, insert a new copy
  else {
    authors[author.name] = author;
  }

}
```

> *Note:* Prior to 2015, Ignia used the [Banner Indent Style](http://en.wikipedia.org/wiki/Indent_style#Banner_style), which uses an indented trailing brace. Any legacy code being used should be updated to the above standards in bulk before implementation.

<!-- http://en.wikipedia.org/wiki/Indent_style#Variant:_Stroustrup -->

### Line Wrapping
- If *any* elements must be placed on a new line, consider moving *all* elements in the statement to new lines for consistency
- Follow standard indentation rules; subsequent lines should *not* be indented more than two spaces (e.g., to align with a `(` or `=`, for instance)

> *Note:* If variable assignments require multiple lines, they should not be aligned to the ruler; i.e., do not:
```js
let author                      = 'Jorge Luis Borges';
let books                       = [ 'Ficciones',
                                    'Labyrinths',
                                    'El Aleph',
                                    'Poesía completa'
                                  ];
let birthday                    = '1899-08-24';
```

- If function arguments cannot fit on a single line, each should be placed on its own line and indented two spaces
- If expressions must be placed on multiple lines, each new line should begin with the operator (e.g., `+`) and be indented two spaces
- If method chains must be placed on multiple lines, each new line should begin with the period (i.e., `.`) and be indented two spaces
- Do not use leading commas; commas should always appear *after* their preceding statement

```js
var book = new Book(
  'Ficcionnes',
  'Jorge Luis Borges',
  '1994-02-01',
  180
);

book.excerpt =
  'Nosotros, de un vistazo, percibimos tres copas en una mesa; Funes, todos los vástagos y racimos y frutos '
  + 'que comprende una parra. Sabía las formas de las nubes australes del amanecer del 30 de abril de 1882 '
  + 'y podía compararlas en el recuerdo con las vetas de un libro en pasta española que sólo había mirado '
  + 'una vez y con las líneas de la espuma que un remo levantó en el Río Negro la víspera de la acción del '
  + 'Quebracho.';

books
  .save()
  .success(
    function(
      data,
      status,
      headers,
      config
    ) {
    ...
    }
  )
```
> *Note:* The above is intended to illustrate the standards; in practice, multi-line strings should not use string concatenation.

## Comments
- Use documentation-style comments as permitted by each language (e.g., XmlDoc in C#)
- Use `/* ... */` syntax for multi-line comments *unless required otherwise by documentation format*

> *Note:* Prior to 2015, Ignia used flower-boxes for comments. These should be replaced with documentation-style comments when updating legacy code.





