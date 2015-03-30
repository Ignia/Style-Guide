# ECMAScript 6.0

ECMAScript is the standard behind JavaScript. ECMAScript 6.0 (sometimes, incorrectly, referred to as JavaScript 6.0) is a significant update - arguably the most significant in the history of the language - and introduces a lot of new syntax, types, and capabilities. While most browsers do not yet support ECMAScript 6, Ignia is developing for it today using transpilers such as [Google Traceur](https://github.com/google/traceur-compiler) and [Babel](https://babeljs.io/).

> *Note:* This style guide inherits rules from the [JavaScript Style Guide](./README.md), [C-Based Languages Style Guide](../README.md), and the [Global Style Guide](../../README.md)

> # Placeholder Content
> This page is a placeholder; additional content will be provided at a later date.

<!--
-->

## Contents
- [Identifiers](#identifiers)
- [Spacing](#spacing)
- [Formatting](#formatting)
- [Language Features](#language-features)
- [Acknowledgments](#acknowledgments)

## Spacing

## Formatting

## Language Features
- Always use `let` instead of `var`; it follows more predictable scoping and hoisting rules, particularly in loops, and prevents accidental redeclaration of global variables
- Always use `set` when defining genuine constants
- Only use the `u` flag when performing regular expressions on strings including 16-bit characters; it is not performant
- Prefer `includes()`, `startsWith()` and `endsWith()` to `indexOf()` when operating against strings, and the index of the match is not needed
- Prefer using `object.is()` to `===` for evaluating identicality; it is more readable, and mitigates edge cases with `NaN`, `-0` and `+0`
- Consider using array destructuring as a more readable alternative to hard-coding indexes (e.g., `array[3]`) if the values are not expected to change within the variable scope; e.g.,

```js
let users = [['Jeremy', 'Caney', 'Architect'], ['Katherine', 'Trunkey', 'Developer']];
for (let i=0; i < users.length; i++) {
  let [firstName, lastName, title] = users[i];
  console.log(firstName + " " + lastName + "(" + title + ")");
}
```

- Make use of default parameters in method calls to clearly communicate what is optional, and to simplify setting defaults; when using default parameters, however, it may still be necessary to check for `null` values
- Prefer use of rest parameters (i.e., `...array`) over the `parameters` collection
- If using destructured parameters, always provide a default, even if it's just an empty object; otherwise, an error will be thrown if the object is not passed
- For handling option parameters, prefer use of `Object.assign()` over destructured parameters, as this keeps variables maintained in an object
- Prefer `Object.assign()` to framework-specific mixin or extends methods (e.g., `angular.extend()` or `angular.merge()`)
- Avoid passing anonymous function expressions as callbacks; instead, use either arrow functions (e.g., `(param1, param1) => param1 + param2`) or references to named functions
- When defining objects using object literal syntax, prefer the new method intializer shorthand (e.g., `getValue() {}` instead of `getValue: function() {}`)
- Use `super` instead of `Object.getPrototypeOf(this)` to call the base method from the object's prototype
- Prefer use of symbols (e.g., `Symbole('private')`) to naming conventions (e.g., `_private`) to hide members from `getOwnPropertyNames()`
- If a collection contains unique items and there is no need to retrieve (*or set*) individual records by an indexer, prefer `Set` over `Array`
- For associative arrays (e.g., dictionaries) prefer `Map` over `Object`; these allow non-string keys (e.g., integers, objects), honor order, and allow for members to be defined independent of values (e.g., to add a `filter()` method)



> *Note:* When relying on transpilers for backward compatibility support, carefully test new language features to ensure they are handled correctly.


## Acknowledgments
- [Understanding ECMAScript 6](https://leanpub.com/understandinges6/read/) by [Nicholas Zakas](https://github.com/nzakas/)