# Angular Style Guide

While Angular follows best practices for [JavaScript](./Readme.md), it introduces some unique considerations with regard to Angular-specific concepts such as service, controllers, and $scope variables.

> *Note:* This style guide inherits rules from the [JavaScript Style Guide](./README.md), [C-Based Languages Style Guide](../README.md), and the [Global Style Guide](../../README.md)

## Contents
- [Identifiers](#identifiers)
- [Formatting](#formatting)
- [Files](#files)
- [Language Features](#language-features)
  - [Controllers and Routes](#controllers-and-routes)
  - [Services](#services)
  - [Directives](#directives)
- [Acknowledgments](#acknowledgments)

## Identifiers
- Controllers and factories should be PascalCase (as they represent a constructor); all other object identifiers (e.g., directives, services) should be camelCase
- Controllers should be suffixed with `Controller` (e.g., `HomeController`)
- The primary module for an application should be named `app`; if, later, sub-modules are needed, they should be named `app.subModule` (e.g., `app.admin`)
- Use a (short) prefix for directives to avoid naming conflicts; do not use the `ng-` or `ui-` prefixes (these are reserved for Angular and Angular UI respectively)
- Do not prefix methods or properties in controllers or services with `$` (this is reserved for Angular)

## Formatting

## Files
- Place each module, directive, service, and controller in its own file
- Separate source files into `Directives`, `Services`, and `Controllers` directories
- Module definitions should occur in the root of the application's `scripts` directory and should be named with the suffix `.Module.js` (e.g., `app.Module.js`); this makes it easy to target them first as part of a concatenation process
- Module files should only contain the module declaration and any global configuration settings or constants for that module
- Routes should be placed in their own file (e.g., `app.Routes.js`) and be placed in the root of the application's `scripts` directory; this provides a convenient "manifest" of controllers

## Language Features
- Do not store modules in a global variable; instead, instantiate them using `angular.module('Name', [])` and extend them using `angular.module('Name')`
- Enclose Angular scripts in an immediately-invoked function expression (IIFE) in order to prevent unnecessary polluting of the global scope
- Always include dependency injection parameters using optional array format (e.g., `angular.controller('Name', ['$service', function ($service) { ... }])`), `$inject` *or* [ngAnnotate](https://github.com/olov/ng-annotate)'s `/* @ngInject */` annotation; these methods ensure compatibility with code obfuscation (e.g., [UglifyJS](http://lisperator.net/uglifyjs/))
- Do not use function expressions (e.g., `function() {}`) for public methods; instead, use function declarations (e.g., `function methodName() {}`) ([source](https://github.com/johnpapa/angular-styleguide#style-y034))
- When chaining multiple promises, consider adding a `catch()` handler to centralize error handling
- Prefer `ng-bind` (or `ng-cloak`) to `{{interpolation}}` in views to ensure that binding expressions are not temporarily displayed while loading the Angular controller
- Always use the `ng-src`, `ng-href` or `ng-style` directives when binding dynamic content to images, links, or styled elements respectively
- If data-bound attributes do not need to be updated after the initial digest cycle, use the [one-time binding](https://docs.angularjs.org/guide/expression#one-time-binding) syntax (e.g., `::property`); this improves performance
- For performance reasons, avoid using `$watch` unless absolutely necessary; for collections, prefer `$watchCollection` unless deep watching is required by the application; for very large collections, consider using [angular-immutable](http://blog.mgechev.com/2015/03/02/immutability-in-angularjs-immutablejs/)

> *Consider* using a thin app module with features being broken out into sub-modules ([source](https://github.com/johnpapa/angular-styleguide#keep-the-app-module-thin)), each with their own app manifest ([source](https://github.com/johnpapa/angular-styleguide#module-dependencies))

```js
(function() {
  'use strict';

  angular
    .module('app', [])
    .factory('bookService', bookService)

  bookService.$inject = ['$resource'];

  function bookService($resource) {

    var service = {
      this.total = 0;
      this.getBooks = getBooks;
    }

    return service;

    function getBooks(authorName) {
      ...
    }

  }

}());
```

### Controllers and Routes
- Centralize reusable logic in services; controllers should only contain minimal view-specific logic
- When using `ng-route`, prefer `controllerAs` to relying on `$scope` (this allows scope variables to be assigned to `this`)
  - Use a consistent object name for `ControllerAs` (e.g., `model`), and assign it to `this` within controllers; e.g., `var model = this;`
- Wrap intialization logic in an `init()` method within controllers to keep logic centralized and simplify refresh requirements ([source](https://github.com/johnpapa/angular-styleguide#controller-activation-promises))
- Use [AngularUI Router](http://angular-ui.github.io/ui-router/) for routing, as it supports nested views (if needed)

### Services
- Use factories instead of services; the syntax is similar, but factories are more flexible; if centralized configuration is needed, then use a provider
- Define the returnable object at the top of a factory or directive, to establish its public interface; all methods should point to function declarations after the returned object
- If a service method executes a promise, prefer returning the promise so it can be chained by the caller
- Decorate the `$exceptionHandler` service using the `$provide` service to institute global custom exception handling ([source](https://github.com/johnpapa/angular-styleguide#decorators))
- Reusable blocks (e.g., exception handling, logging, security, and local data storage) are needed across multiple applications, and should be stored in their own modules ([source](https://github.com/johnpapa/angular-styleguide#reusable-blocks-are-modules))
- Use the [`$cacheFactory` service](https://docs.angularjs.org/api/ng/service/$cacheFactory) to provide session-based caching of expensive operations; note that this is handled automatically by `$http` and `$resource`

### Directives
- Do not provide DOM manipulation from a controller; use directives instead (e.g., existing directives such as `ng-show` or custom directives)
- Prefer assigning directives to elements (`restrict: 'E'`) and optionally attributes (`restrict: 'A'`) over classes (`restrict: 'S'`) ([source](https://github.com/johnpapa/angular-styleguide#restrict-to-elements-and-attributes))
- When using Bootstrap, use the [AngularUI Bootstrap directives](https://angular-ui.github.io/bootstrap/); this provides more succinct coverage of Bootstrap markup and classes
- Always use the [$sce service](https://docs.angularjs.org/api/ng/service/$sce) and, if appropriate, the [`ngSanitize` module](https://docs.angularjs.org/api/ngSanitize) when relying on user inputted code (these are accounted for by default in first-party directives, such as [`ngBindHtml`](https://docs.angularjs.org/api/ng/directive/ngBindHtml))

<!--
Consider using: Mocha (testing), Chai (assertions), Karma (test runner), and Sinon (stubbing), and PhantomJS ("headless browser"); see https://github.com/johnpapa/angular-styleguide#testing
-->

<!--
## Comments
- Evaluate: [ngDocs](https://github.com/angular/angular.js/wiki/Writing-AngularJS-Documentation) and [dgneni](https://github.com/angular/dgeni) for AngularJS documentation
-->

## Acknowledgments
- [Angular Style Guide](https://github.com/johnpapa/angular-styleguide) by [John Papa](https://github.com/johnpapa)
- [AngularJS Style Guide](https://github.com/mgechev/angularjs-style-guide) by [Minko Gechev](https://github.com/mgechev)
