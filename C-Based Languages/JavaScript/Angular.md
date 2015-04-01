# Angular Style Guide

While Angular follows best practices for [JavaScript](./Readme.md), it introduces some unique considerations with regard to Angular-specific concepts such as services, controllers, and $scope variables.

> *Note:* This style guide inherits rules from the [JavaScript Style Guide](./README.md), [C-Based Languages Style Guide](../README.md), and the [Global Style Guide](../../README.md). If using ECMAScript 6, the [ECMAScript 6 Style Guide](./ECMAScript%206.md) should also be honored.

## Contents
- [Identifiers](#identifiers)
- [Formatting](#formatting)
- [Files](#files)
- [Language Features](#language-features)
  - [Data Binding](#data-binding)
  - [Controllers and Routes](#controllers-and-routes)
  - [Services](#services)
  - [Directives](#directives)
- [Acknowledgments](#acknowledgments)

## Identifiers
- Controllers and factories should be PascalCase (as they represent class constructors); all other object identifiers (e.g., directives, services) should be camelCase
- Controllers should be suffixed with `Controller` (e.g., `HomeController`); do not use `Ctrl` or some other abbreviation
- The primary module for an application should be named `app`; if sub-modules are needed, they should be named `app.subModule` (e.g., `app.admin`)
- Use a (short) namespace prefix for directives to avoid naming conflicts; do not use the `ng-` or `ui-` prefixes (these are reserved for Angular and Angular UI respectively)
- Do not prefix methods or properties in controllers or services with `$` (this is reserved for Angular and jQuery)

## Formatting

## Files
- Place each module, directive, service, and controller in its own file
- Separate any centralized source files into `Directives`, `Services`, and `Controllers` directories

> *Note:* For larger applications, organize files according to feature (e.g., Home, Account, Profile) instead of by type (e.g., Directives, Services, Controllers) ([source](https://docs.google.com/document/d/1XXMvReO8-Awi1EZXAXS4PzDzdNvV6pGcuaF4Q9821Es/pub)) so that applications can be assembled (or disassembled) using modules as functional blocks

- When using multiple modules, the folder structure should mirror the module structure
- Module definitions should occur in the root of a module's folder (e.g., `app`) and be named with the suffix `.Module.js` (e.g., `app.Module.js`); this makes it easy to target them first as part of a concatenation process
- Module files should only contain the module declaration and any global configuration settings or constants for that module

> *Note:* For larger applications, configuration settings and constants should be broken out into their own files (e.g., `app.Config.js`, `app.Constants.js`)

- Routes should be placed in their own file (e.g., `app.Routes.js`) and be placed in the root of the application's `scripts` directory; this provides a convenient "manifest" of controllers

## Language Features
- Only include jQuery if advanced features are needed; Angular includes a "lite" version of jQuery which supports most basic features
  - If jQuery *is* needed, it must be included *before* the Angular scripts
- Do not store modules in a global variable (e.g., `var module = angular.module(`module`, [])`); instead, instantiate them using `angular.module('module', [])` and extend them using `angular.module('module')`
- Enclose Angular scripts in an immediately-invoked function expression (IIFE) in order to prevent unnecessary polluting of the global scope
- Always include dependency injection parameters using the optional array format (e.g., `angular.controller('Name', ['$service', function ($service) { ... }])`), `$inject`, *or* [ngAnnotate](https://github.com/olov/ng-annotate)'s `/* @ngInject */` annotation; these methods ensure compatibility with code obfuscation (e.g., [UglifyJS](http://lisperator.net/uglifyjs/))
- Do not use function expressions (e.g., `function() {}`) for public methods; instead, use function declarations (e.g., `function methodName() {}`); this allows the public interface to be summarized at the top of a file, with implementation details provided later ([source](https://github.com/johnpapa/angular-styleguide#style-y034))
- When chaining multiple promises, consider adding a `catch()` handler to centralize error handling
- Only use `$broadcast()`, `$emit()` and `$on()` for events that need to be globally accessible; prefer using `$scope.$watch`, services, or directive-controllers for internal communication ([source](https://github.com/angular/angular.js/wiki/Best-Practices))
- Use `$scope.$on('$destroy', ...)` for garbage collection on controllers and directives to remove any plugins or listeners in single-page applications

> *Consider* using a thin app module with features being broken out into sub-modules ([source](https://github.com/johnpapa/angular-styleguide#keep-the-app-module-thin)), each with their own app manifest ([source](https://github.com/johnpapa/angular-styleguide#module-dependencies)).

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

### Data Binding
- Prefer `ng-bind` (or `ng-cloak`) to `{{interpolation}}` in views to ensure that binding expressions are not temporarily displayed while loading the Angular controller
- Always use the `ng-src`, `ng-href`, or `ng-style` directives when binding dynamic content to images, links, or styled elements respectively
- If data-bound attributes do not need to be updated after the initial digest cycle, use the [one-time binding](https://docs.angularjs.org/guide/expression#one-time-binding) syntax (e.g., `::property`); this improves performance
- For performance reasons, avoid using `$watch` unless absolutely necessary
  - For collections, prefer `$watchCollection` unless deep watching is required by the application
  - For very large collections, consider using [angular-immutable](http://blog.mgechev.com/2015/03/02/immutability-in-angularjs-immutablejs/)

### Controllers and Routes
- Centralize reusable logic in services; controllers should only contain minimal view-specific logic
- When using `ng-route`, prefer `controllerAs` to relying on `$scope` (this allows scope variables to be assigned to `this`)
  - Use a consistent object name for `ControllerAs` (e.g., `model`), and assign it to `this` within controllers; e.g., `var model = this;`
- Wrap intialization logic in an `init()` method within controllers to keep logic centralized and simplify refresh requirements ([source](https://github.com/johnpapa/angular-styleguide#controller-activation-promises))
- Use [AngularUI Router](http://angular-ui.github.io/ui-router/) for routing, as it supports nested views (if needed)

### Services
- Use factories instead of services: the syntax is similar, but factories simplify separation of implementation details; if centralized configuration is needed, then use a provider
- Define the returnable object at the top of a factory or directive to establish its public interface; all methods should point to function declarations after the returned object (see code sample above)
- If a service method executes a promise, prefer returning the promise to the value so it can be chained by the caller
- To institute global custom exception handling, decorate the `$exceptionHandler` service using the `$provide` service ([source](https://github.com/johnpapa/angular-styleguide#decorators))
- Reusable blocks (e.g., exception handling, logging, security, and local data storage) needed across multiple applications  should be stored in their own modules ([source](https://github.com/johnpapa/angular-styleguide#reusable-blocks-are-modules))
- Use the [`$cacheFactory` service](https://docs.angularjs.org/api/ng/service/$cacheFactory) to provide session-based caching of expensive operations; note that this is handled automatically by `$http` and `$resource`

### Directives
- Do not provide DOM manipulation from a controller; use directives instead (e.g., existing directives such as `ng-show` or custom directives)
- Prefer assigning directives to elements (`restrict: 'E'`) and optionally attributes (`restrict: 'A'`) over classes (`restrict: 'S'`) ([source](https://github.com/johnpapa/angular-styleguide#restrict-to-elements-and-attributes))
  - Prefer instantiating directives as elements if they are acting as a control (e.g., `ui-date-picker`), and attributes for modifiers (e.g., `ng-model`)
  - If HTML validation is critical, define all directives as elements prefixed with `data-` (e.g., `data-ng-model`)
- When using Bootstrap, use the [AngularUI Bootstrap directives](https://angular-ui.github.io/bootstrap/); this provides more succinct coverage of Bootstrap markup and classes
- Always use the [$sce service](https://docs.angularjs.org/api/ng/service/$sce) and, if appropriate, the [`ngSanitize` module](https://docs.angularjs.org/api/ngSanitize) when relying on user inputted markup (these are accounted for by default in first-party directives, such as [`ngBindHtml`](https://docs.angularjs.org/api/ng/directive/ngBindHtml))
- Use the [`$observe()` method](https://docs.angularjs.org/api/ng/type/$compile.directive.Attributes#$observe) to ensure expressions can be effectively used in attribute values

<!--
Consider using: Mocha (testing), Chai (assertions), Karma (test runner), Sinon (stubbing), and PhantomJS ("headless browser"); see https://github.com/johnpapa/angular-styleguide#testing
-->

<!--
## Comments
- Evaluate: [ngDocs](https://github.com/angular/angular.js/wiki/Writing-AngularJS-Documentation) and [dgneni](https://github.com/angular/dgeni) for AngularJS documentation
-->

## Acknowledgments
- [Angular Style Guide](https://github.com/johnpapa/angular-styleguide) by [John Papa](https://github.com/johnpapa)
- [AngularJS Style Guide](https://github.com/mgechev/angularjs-style-guide) by [Minko Gechev](https://github.com/mgechev)
- [AngularJS Style Guide for Closure Users at Google](https://google-styleguide.googlecode.com/svn/trunk/angularjs-google-style.html)
- [AngularJS Best Practices](https://github.com/angular/angular.js/wiki/Best-Practices)