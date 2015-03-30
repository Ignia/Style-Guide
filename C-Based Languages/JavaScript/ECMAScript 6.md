# ECMAScript 6.0

ECMAScript is the standard behind JavaScript. ECMAScript 6.0 (sometimes, incorrectly, referred to as JavaScript 6.0) is a significant update - arguably the most significant in the history of the language - and introduces a lot of new syntax, types, and capabilities. While most browsers do not yet support ECMAScript 6, Ignia is developing for it today using transpilers such as [Google Traceur](https://github.com/google/traceur-compiler) and [Babel](https://babeljs.io/).

> *Note:* This style guide inherits rules from the [JavaScript Style Guide](./README.md), [C-Based Languages Style Guide](../README.md), and the [Global Style Guide](../../README.md)

> *Note:* The ECMAScript 6 standard is not yet finalized, and some implementation details are expected to change before publication; the guidance below will be reevaluated at that point to ensure consistency with the final direction.

## Contents
- [Language Features](#language-features)
  - [Variables](#variables)
  - [Classes, Objects, and Prototypes](#classes-prototypes-and-objects)
  - [Functions and Methods](#functions-and-methods)
  - [Collections and Arrays](#collections-and-arrays)
- [Acknowledgments](#acknowledgments)

## Language Features
- Prefer `includes()`, `startsWith()` and `endsWith()` to `indexOf()` when operating against strings, and the index of the match is not needed
- Prefer template strings (e.g., `` `By ${name}` ``) to string concatenation (e.g., `'By ' + name`)
- Prefer using `object.is()` to `===` for evaluating identicality; it is more readable, and mitigates edge cases with `NaN`, `-0` and `+0`
- Only use the `u` flag when performing regular expressions on strings including 16-bit characters; it is not performant

### Variables
- Always use `let` instead of `var`; it follows more predictable scoping and hoisting rules, particularly in loops, and prevents accidental redeclaration of global variables
- Always use `set` when defining genuine constants
- Consider using array destructuring as a more readable alternative to hard-coding indexes (e.g., `array[3]`) if the values are not expected to change within the variable scope; e.g.,

```js
let users = [['Jeremy', 'Caney', 'Architect'], ['Katherine', 'Trunkey', 'Developer']];

for (let i=0; i < users.length; i++) {
  let [firstName, lastName, title] = users[i];
  console.log(firstName + " " + lastName + "(" + title + ")");
}
```
### Classes, Prototypes, and Objects
- Prefer use of symbols (e.g., `Symbol('private')`) to naming conventions (e.g., `_private`) to hide members from `getOwnPropertyNames()`
- Consider using `Proxy` classes when specific business logic needs to be applied to all properties in a class (e.g., for validation, such as type safety), potentially including properties not yet instantiated (e.g., for lazy loading)
- Prefer `Object.assign()` to framework-specific mixin or extends methods (e.g., `angular.extend()` or `angular.merge()`)
- When defining objects using object literal syntax, prefer the new method intializer shorthand (e.g., `getValue() {}` instead of `getValue: function() {}`)
- Use `super` instead of `Object.getPrototypeOf(this)` to call the base method from the object's prototype

### Functions and Methods
- If using destructured parameters, always provide a default, even if it's just an empty object; otherwise, an error will be thrown if the object is not passed
- Make use of default parameters in method calls to clearly communicate what is optional, and to simplify setting defaults; when using default parameters, however, it may still be necessary to check for `null` values
- Prefer use of rest parameters (i.e., `...array`) over the `parameters` collection
- For handling option parameters, prefer use of `Object.assign()` over destructured parameters, as this keeps variables maintained in an object
- Avoid passing anonymous function expressions as callbacks; instead, use either arrow functions (e.g., `(param1, param1) => param1 + param2`) or references to named functions

### Collections and Arrays
- If a collection contains unique items and there is no need to retrieve (*or set*) individual records by an indexer, prefer `Set` over `Array`
- For associative arrays (e.g., dictionaries) prefer `Map` over `Object`; these allow non-string keys (e.g., integers, objects), honor order, and allow for members to be defined independent of values (e.g., to add a `filter()` method)
- Prefer `for-of` style iteration to traditional `for` loops; with iterators, the behavior is standardized across `Array`, `Object`, `Set`, `Map`, and even `NodeList`

> *Note:* When relying on transpilers for backward compatibility support, carefully test new language features to ensure they are handled correctly.

## Acknowledgments
- [Understanding ECMAScript 6](https://leanpub.com/understandinges6/read/) by [Nicholas Zakas](https://github.com/nzakas/)