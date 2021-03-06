# HTML5 Style Guide

> *Note:* This style guide inherits rules from the [SGML-Based Languages Style Guide](./README.md) and the [Global Style Guide](../README.md). For images, it also assumes compliance with the [Media Files Style Guide](../Media%20Files/README.md). This document supersedes our legacy [Production Standards](../Legacy/Production.Standards.doc?raw=true) and [HTML Style Guide](../Legacy/HTML.StyleGuide.doc?raw=true) documents (Microsoft Word).


## Contents
- [General Principles](#general-principles)
- [Formatting](#formatting)
- [Semantics](#semantics)
- [Encoding](#encoding)
- [Acknowledgments](#acknowledgments)

## General Principles
> "Strive to maintain HTML standards and semantics, but not at the expense of practicality. Use the least amount of markup with the fewest intricacies whenever possible." - [Mark Otto](http://markdotto.com/about/) ([source](http://mdo.github.io/code-guide/#html-practicality))

## Formatting
- It is recommended to use [Mark Otto](http://markdotto.com/about/)'s proposed [attribute order](http://mdo.github.io/code-guide/#html-attribute-order)

## Language Features
- Always begin the document with the doctype (i.e., `<!DOCTYPE html>`)
- Always include optional elements (e.g., `html`, `head`, `body`)
- If setting content type, always use `text/html` (even for XHTML)
- Explicitly close tags where closing tag is optional (e.g., `<p>`, `<li>`)
- Use self-enclosing syntax for "void" elements (e.g., `<br />`, `<hr />`)
- Do not include attribute value for Boolean attributes (e.g., `<input disabled />`)
- Always provide an `alt` element for multimedia content (e.g., `<img>`, `<audio>`, `<video>`)
- Prefer `<svg>` to `<canvas>` unless performance is a key concern (e.g., 100+ elements)
- Omit `type` attribute for `<link>`, `<script>` or `<style>` elements
- Always define `rel` attribute for `<link>` element; define when appropriate for `<a>` element
- Always define a `lang` attribute on the `<html>` element
- Always wrap `<input>` elements with a `<label>` element (no need for the `for` attribute in this usage)
- Elements that must exist no more than one time should be identified using `id`; otherwise `class`

## Semantics
- Always use semantic tags when available (e.g., `<button>` over `<div class="button" />`)
- Every page should have one (and exactly one) `<main>` element identifying the primary content
- Every page should have *at least* one `<header>`, `<footer>`, `<nav>`, and `<article>` element
- For a detail page, the `<main>` element will typically include an `<article>` element, which may include multiple `<section>` elements
- For an index of pages or comments, use an `<article>` element for each item; in this case, the `<article>` elements may be wrapped in a `<section>` element
- Headings (e.g., `h1`-`h6`) should be used to denote outline, not (just) style; use a class modifier to alter a style rather than skipping a heading
- The `<section>`, `<article>`, and `<aside>` effectively encapsulate a node in the outline; headings can optionally be "reset" within them (i.e., start back at `h1`) if preferred (not required)
- At minimum, set ARIA `role` attributes on HTML5 semantic elements (e.g., `<header role="banner">`)
- When no meaningful semantic tags are otherwise available, authors are *strongly encouraged* to decorate markup with [Schema.org](http://schema.org) types
  - Prefer using [RDFa lite](http://rdfa.info/) syntax over [Microdata](http://www.w3.org/TR/microdata/) or [Microformats](http://microformats.org/); RDFa is extensible into other vocabularies, and is no more verbose than Microdata
- Attempt to limit `<div>` elements for presentational requirements (e.g., changing positioning); otherwise, prefer semantic elements
- Use [HTML5 Shim](https://github.com/aFarkas/html5shiv) to ensure backward compatibility with Internet Explorer

## Encoding
- Always set encoding to UTF-8 (i.e., via `<meta charset="utf-8">`)
- Take advantage of UTF-8 encoding; do not use entity-references unless required (e.g., for HTML escaping)

## Acknowledgments
- [Code Guide by @mdo](http://mdo.github.io/code-guide/) by [Mark Otto](http://markdotto.com/about/)
- [Google HTML/CSS Style Guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)
- [Front-end Code Standards & Best Practices](http://isobar-idev.github.io/code-standards/) by [isobar](http://www.isobar.com/)
