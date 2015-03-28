# JavaScript Style Guide

## Style Guides
- [Angular](./Angular.md)
- [ECMAScript 6.0](./ECMAScript%206.md)
- [TypeScript](./TypeScript.md)
- [JSON](./JSON.md) (and JavaScript object literal notation)

> *Note:* This style guide inherits rules from the [C-Based Languages Style Guide](../README.md), and the [Global Style Guide](../../README.md)

## Contents
- [Identifiers](#identifiers)
- [Variables](#variables)
- [Syntax](#syntax)
- [Language Features](#language-features)
- [Comments](#comments)
- [Acknowledgments](#acknowledgments)

## Identifiers
- Class members (e.g., properties, functions) and namespaces should be `camelCase` (e.g., `doSomething()`)
- Use `_this` as the variable name when saving a reference to `this` (although `.bind()` for scoping is preferred)

## Variables
- Always declare variables using `var` (enforced in `use strict`)


## Syntax
- Always end lines with semicolons; do not rely on implicit insertion ([source](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=Semicolons#Semicolons))
- Use single quotes for string values, not double quotes; this helps avoid the need for escaping
- Only access properties using subscript notation (i.e., `[]`) when the property name is variable
- Use `===` and `!==` over `==` and `!=` as these are more precise and predictable
- Name functions to aid in debugging (i.e., so functions are identified in stack traces)


## Language Features
- Namespaces should be used when possible, using either library features or an object wrapper
- Do not use `eval()` or Internet Explorer's conditional comments (e.g., `/*@cc_on ... @*/`)
- Do not use `for in` loops for arrays ([source](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=for-in_loop#for-in_loop))
- Do not use wrapper objects for primitive types (e.g., `new Boolean(true)`); casting is fine
- When possible, use JavaScript's boolean expressions (e.g., `if (variable) {}`) ([source](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=Tips_and_Tricks#Tips_and_Tricks))
- Use the literal syntax for creating objects (e.g., `{}` not `new Object()`) and arrays (e.g., `[]` not `new Array()`)
- Assign methods to the prototype object, instead of overwriting the prototype with a new object
- Use proper feature detection instead of relying on user agents; [Modernizr](http://modernizr.com/) encouraged

<!--
- Use function expressions (e.g., `var callback = function() {}` over function declarations (e.g., `function callback() {}`)
  - The exception is constructors, which  use function declarations with the object name
  Consider: JSCS for code style consistency? https://github.com/johnpapa/angular-styleguide#use-an-options-file-1
-->

## Comments
- Use JSDoc-style comments to allow for optional generation of documentation
- If namespaces are used (e.g., with framework modules) use `namespace` and `memberOf` to provide documentation

```
/**
 * FILE TITLE
 * @desc Description
 * @param {string} Parameter description
 * @return {number} Return description
 */
```

## No Opinion
- Declaring one variable per `var` v. multiple variables
- Use of accessor functions for properties

## Acknowledgments
- [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [jQuery JavaScript Style Guide](http://contribute.jquery.org/style-guide/js/)

<!--
- [Mozilla Coding Style](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Coding_Style)
- [WordPress JavaScript Coding Standards](https://make.wordpress.org/core/handbook/coding-standards/javascript/)
- [Code Conventions for the JavaScript Programming Language](http://javascript.crockford.com/code.html) by Douglas Crockford
- [Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js/#whitespace)
-->

