# Sass Style Guide

Sass provides a preprocessor environment for simplifying the creating and maintenance of CSS.

> *Note:* This style guide inherits rules from the [CSS-Based Languages Style Guide](./README.md) and the [Global Style Guide](../README.md).

## Contents
- [Structure](#structure)
- [Spacing](#spacing)
- [Variables](#variables)
- [Comments](#comments)
- [Language Features](#language-features)
- [Declaration Order](#declaration-order)

## Structure
- Establish a `/_variables.scss` for establishing variables
- Break up styles into logically organized files; e.g.,
  - Base (for global overrides for elements)
  - Components (for styling reusable components or controls)
  - Helpers (for functional code, such as mixins, placeholders, and functions)
  - Layout (for structural code, such as grids, positioning, and dimensions)
  - Overrides (for any overrides required of third-party stylesheets)
  - Vendor (for any third-party stylesheets)
  - Views (for any page-specific styles)
- When practical, separate mixins, placeholders, and functions into their own files
- Compile distinct themes, layouts, and page-level CSS independent of the main CSS file
- Do *not* group media queries into a single file (e.g., `_mobile.scss`); they should be associated with the styles they affect
- `_*.scss` files should _either_ be manifests (with `@import` statements) _or_ stylesheets; they should not include both

> *Note:* For more information, see [Ignia's Sass Structure](https://github.com/Ignia/Sass-Structure).

## Spacing
- Indent nested selectors by two spaces

> *Note:* Avoid more than three levels of nesting for both readability and specificity

## Variables
- When introducing a new variable, also add it to the `_variables.scss` in the Sass root directory
  - Also use this file to override variables defaults, as appropriate, from third-party libraries (e.g., Foundation)
- When introducing a new variable in a file, declare the variable at the top of the file with a `!default` flag

> *Note:* The `!default` value will only be used if the variable isn't otherwise defined; this ensures that the styles will work correctly even if their corresponding variables are removed from `_variables.scss`.

## Comments
- Favor single-line comment format (`//`) over the multi-line comment format (`/* */`)

```sass
//==============================================================================================
// LEVEL 1
//----------------------------------------------------------------------------------------------
// Optional description
//==============================================================================================

//----------------------------------------------------------------------------------------------
// LEVEL 2
//----------------------------------------------------------------------------------------------

// Level 3
```

> *Note:* Single-line comments (`//`) are not compiled to the resulting CSS and thus ensure comments are private and not contributing to the size of the CSS file.

## Declaration Order
- Place `@extend` statement on the first line of a declaration block
- When possible, place `@include` statements after `@extend`
- When possible, place `@import` statements at the top of the file

```sass
.selector {
  @extend %placeholder;
  @include clearfix();
  @include border-radius(10px);
  padding: 10px;
  background-color: $background-color;
}
```

## Language Features
- Do not manually prefix declarations or use mixins exclusively for this purpose; this is a task best suited for build tools
- Be wary of excessive nesting; this is a useful feature, but can lead to excessive specificity or granularity
- Generate source maps during compilation and minification to simplify debugging
