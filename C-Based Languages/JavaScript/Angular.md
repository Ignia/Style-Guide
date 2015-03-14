# Angular Style Guide

While Angular follows best practices for [JavaScript](./Readme.md), it introduces some unique considerations with regard to Angular-specific concepts such as service, controllers, and $scope variables.

> # Placeholder Content
> This page is a placeholder; additional content will be provided at a later date.

## Files
- Place each module, directive, service, and controller in its own file
- Separate source files into a `Directives`, `Services`, and `Controllers` directories

## Language Features
- Do not store modules in a global variable; instead, instantiate them using `angular.module('Name', [])` and extend them using `angular.module('Name')`
- Always include dependency injection parameters using optional array format (e.g., `angular.controller('Name', ['$service', function ($service) { ... }])`); this ensures compatibility with code obfuscation (e.g., [UglifyJS](http://lisperator.net/uglifyjs/))
- Centralize reusable logic in services; controllers should only contain minimal view-specific logic

## Acknowledgments
- [AngularJS Style Guide](https://github.com/mgechev/angularjs-style-guide) by [Minko Gechev](https://github.com/mgechev)

