# JSON Style Guide

JSON (JavaScript Object Notation) is a data format supported natively in JavaScript, but also used across other languages. While it is integrated deeply with JavaScript, it follows some formatting rules and limitations that are unique to it and merit separate evaluation. In addition, while some of the characteristics of JSON also apply to other JavaScript objects (such as arrays containing other arrays or objects), these are best evaluated as part of JSON, where these scenarios are most common.

> *Note:* Technically, JSON is a subset of the object literal notation that appears within JavaScript. This style guide addressed both. Where the two diverge, the differences will be noted.

## Identifiers
- Property names ("keys") should always be in double quotes (some libraries do not enforce this, but it is a requirement of the [specificationn](http://tools.ietf.org/html/rfc7159)); this is not required for object literal notation

## Spacing
- Objects in arrays should each begin on a new line

## Formatting
- Commas should immediately follow the closing brace (for objects) or bracket (for arrays)

> *Note:* Spacing and formatting rules are not enforced for JSON delivered externally (e.g., by a REST API); it is expected such JSON will be minified.

## Comments
- Comments are *not* supported in JSON files; if comments are required, it is recommended that they be placed in a property with the name `__comment`
- Comments *are* honored as part of JavaScript's object literal notation, and are welcome contributions for providing inline documentation

## Language Features

## Acknowledgments
- [RFC 7159](http://tools.ietf.org/html/rfc7159)