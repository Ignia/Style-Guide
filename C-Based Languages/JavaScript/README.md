# JavaScript Style Guide

## Identifiers
- Class members (e.g., properties, functions) should be camelCase (e.g., `doSomething()`)
- Namespaces should be PascalCase

## Variables
- Always declare variables using `var` (enforced in `use strict`)

## Syntax
- Always end lines with semicolons; do not rely on implicit insertion ([source](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=Semicolons#Semicolons))
- Use single quotes for string values, not double quotes; this helps avoid the need for escaping

## Language Features
- Namespaces should be used when possible, using either library features or an object wrapper
- Do not use `eval()` or Internet Explorer's conditional comments (e.g., `/*@cc_on ... @*/`)
- Do not use `for in` loops for arrays ([source](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=for-in_loop#for-in_loop))
- Use function expressions (e.g., `var callback = `function() {}` over function declarations (e.g., `function callback() {}`)
  - The exception is constructors, which should use function declarations with the object name
- Do not use wrapper objects for primitive types (e.g., `new Boolean(true)`); casting is fine
- When possible, use JavaScript's boolean expressions (e.g., `if (variable) {}`) ([source](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=Tips_and_Tricks#Tips_and_Tricks))

## Comments
- Use JSDoc-style comments to allow for optional generation of documentation

```
/**
 * FILE TITLE
 * @desc Description
 * @param {string} Parameter description
 * @return {number} Return description
 */
```

## Acknowledgments
- [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
-