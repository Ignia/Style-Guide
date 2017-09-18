# CSS-Based Languages

CSS-Based languages include CSS itself, as well as CSS preprocessors such as Sass, Less, and Stylus. Ignia typically uses Less for Bootstrap projects, and Sass for highly-custom user interfaces.

## Style Guides
- [Sass](./Sass.md)

> *Note:* This style guide inherits rules from the [Global Style Guide](../README.md). For images, it also assumes compliance with the [Media Files Style Guide](../Media%20Files/README.md). This document supersedes our legacy [Production Standards](../Legacy/Production.Standards.doc?raw=true) (Microsoft Word).

## Contents
- [Performance](#performance)
- [Identifiers](#identifiers)
  - [Capitalization](#capitalization)
- [Selectors](#selectors)
- [Spacing](#spacing)
- [Formatting](#formatting)
- [Comments](#comments)
- [Declaration Order](#declaration-order)
- [Language Features](#language-features)
- [No Opinion](#no-opinion)
- [Acknowledgments](#acknowledgments)

## Performance
With a few exceptions, maintainability trumps performance with CSS. While performance is a priority, CSS optimizations tend to have minimal impact compared to JavaScript and even HTML optimizations. That said, ancestor and wildcard selectors should be avoided, as should the `@import` directive.

## Identifiers
- Class identifiers should aim to be semantic (e.g., `important`) over presentational (e.g., `red`)
- Hyphens should be used to distinguish associated *concepts* not *words*
- Be wary of compounding concepts via hyphens; cascading may provide more flexibility
- Begin state classes with `.is-` (e.g., `.is-active`)
- Begin JavaScript-exclusive classes with `.js-` (e.g., for selectors), and do *not* reference in stylesheets
- If lack of JavaScript support is a concern, use a `js-hidden` utility class to provide fallback content (and hide using JavaScript)

### Capitalization
- Class identifiers should be in `lisp-case` (lowercase with hyphens)
- Declaration properties and values should be lowercase (e.g., `color: #f1f1f1`)

## Selectors
- Place each selector on its own line (i.e., place a line-break after each `,` in a selector)
- Do not use element identifiers (e.g., `#identifier`) in selectors outside of layout elements (e.g., `#Navigation`, `#Header`), page-specific namespaces (e.g., `#AboutPage`), or theme namespaces (e.g., `#AdminTheme`)
- Avoid nesting selectors more than three levels deep; this introduces specificity issues
  - By convention, nested selectors should follow the pattern: `[#namespace] *component*[.*modifier*] > *element*[.*modifer*]` (e.g., `#RightRail .login.inline .username.error`)
- Target semantic elements and attributes instead of classes where practical (e.g., `button` not `.button`) to enforce semantic markup
  - Avoid assigning classes that duplicate semantic tags (e.g., `<button class="button" />`)
- If class semantics are described by a [Schema.org](http://schema.org/) type, use `[typeof='Type']` and `[property='property'] instead of inventing new class names
- Only combine class names with elements (e.g., `li.is-active`) if the rule is exclusive to that element type
- Avoid ancestor selectors when possible; these can be *very* slow

## Spacing
- Include a single space between a selector and a brace
- Include single space after the colon of a declaration
- Include a space after each comma in comma-separated arguments
- Indent all block content (e.g., nested rules, declarations)
- Separate each rule-set with a blank line
- Set editor to remove trailing space (to simplify diffs)

## Formatting
- Opening brace must be placed on the same line as the last selector
- Closing brace must be on its own line
- Include one declaration per line in a declaration block
- Use one level of indentation for each declaration
- Use single quotation marks for attribute selectors and property values
- Always use quotations when optional (e.g., for attribute selectors, file locations)
- Always specify a leading 0 for decimals (e.g., 0.25, not .25)
- End each declaration with a semi-colon

```css
input:focus,
input:active,
.is-active {
  color: #f00;
  border: 1px solid #f00;
}

```

> *Note:* Large blocks of single declarations may use a single-line format; in this case, pad the declaration with a single space.
```css
.first-selector  { color: #fff }
.second-selector { color: #ccc }
.third-selector  { color: #000 }
```
> *Note:* Line-breaks may optionally be placed after comma-separated values; in this case, each value should be placed on its own line and indented two spaces.
```css
.selector {
  background-image:
    linear-gradient(#000, #ccc),
    linear-gradient(#ccc, #000);
}
```

## Comments
- Use Ignia-style flower-boxes for comments (see below)
- Limit flower-box width to 96 characters (column 97)
- Use Level 1 and 2 comment blocks for grouping related rule-sets
- Only Level 3 comments should be used within rule-sets
- Level 1 and 2 comments should have capitalized titles; optional descriptions should be sentence case
- Comments should always be on their own line(s)

```css
/*==============================================================================================
| LEVEL 1 COMMENT
>-----------------------------------------------------------------------------------------------
| With optional description
\=============================================================================================*/

/*----------------------------------------------------------------------------------------------
| LEVEL 2 COMMENT
\---------------------------------------------------------------------------------------------*/

//Level 3 comment
```
> *Note:* When using a CSS preprocessor, the `//` format should be used instead, in order to prevent comments from being compiled with the CSS. See [Sass Style Guide](./Sass.md).

## Declaration Order
- Declarations should be ordered by:
  1. Positioning (e.g., z-index, top, right),
  2. Box model (e.g., display, overflow, width, margin),
  3. Typographic (e.g., font, font-family, font-size), then
  4. Visual elements (e.g., color, background)

## Language Features
- Use `rem` units for fonts with a `px` fallback for backward compatibility; do not use `em`
- Prefer RGBA (e.g., `rgba(255, 255, 255, 1)` to hexadecimal color format (e.g., `#FFFFFF`); this is easier to manipulate, and supports transparencies
- Do not use `@import`, unless using a preprocessor; it adds extra time to the page load
- Avoid ancestor selectors when possible; these can be *very* slow
- Only use Internet Explorer hacks like `_` and `*` if absolutely required for compatibility (rare)
- Do not set height on elements containing text (and *especially* when used with a CMS or localization)
- Place media queries alongside related classes; do not establish independent CSS files for each target device

## No Opinion
- Indentation of related rule-sets
- Omission of unit specification after 0 values (e.g., `0` v. `0px`)
- Use of shorthand syntax (e.g., `border-color: #000` v. `border: 1px solid #000`)
- Use of 3 v. 6 hexadecimal color format (e.g., `#fff` v. `#ffffff`)

## Acknowledgments
- [Pedantic CSS](http://pedantic-css.readme.io/v1.0)
- [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
- [Google HTML/CSS Style Guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)
- [Code Guide by @mdo](http://mdo.github.io/code-guide/#css)
- [OOCSS Code Standards](https://github.com/stubbornella/oocss-code-standards)
- [Front-end Code Standards & Best Practices](http://isobar-idev.github.io/code-standards/) by [isobar](http://www.isobar.com/)

