# Media Files Style Guide

The following provides guidelines for producing images produced for the web. Future iterations will also cover audio, video, and animation.

> *Note:* This style guide inherits rules from the [Global Style Guide](../README.md). It is also expected, in particular, to be used in conjunction with the [CSS-Based Languages Style Guide](../CSS-Based%20Languages/README.md) and [HTML5 Style Guide](../SGML-Based%Languages/HTML5.md). This document supersedes our legacy [Production Standards](../Legacy/Production.Standards.doc) (Microsoft Word).


## Contents
- [Identifiers](#identifiers)
  - [Folder Structure](#folder-structure)
  - [Naming Conventions](#naming-conventions)
- [Production Standards](#production-standards)
  - [Formats](#formats)

## Identifiers

### Folder Structure
- Images that are shared between many pages should be placed in the root `/Images` directory
- Consider organizing shared images by:
  - `/Icons` for images used to annotate links and navigation on the site; may also be used for "spinners"
  - `/Layout` for images necessary for creating the overall layout (e.g., header, navigation, footer)
  - `/Sprites` for composite images that contain multiple graphics which will be positioned using CSS
  - `/Tiles` for background images such as textures
- Images that are specific to a particular section or feature should be placed in a corresponding images directory (e.g., `/Account/Images` for the `/Account` feature)
- Prefer placing source files (e.g., `*.psd`, `*.ai`) next to output files so they're easy to maintain; these can be filtered out by build automation
  - When working from one large source file, consider creating smaller templates for commonly modified images (e.g., an image that requires localization)
  - Alternatively, consider providing shortcut files to original source locations (e.g., Ignia's `Projects` file share, a partner's [Box](http://box.com) share)

### Naming Conventions
- Image file names should use `PascalCase` and separate *concepts* (not words) by periods (e.g., `AmazonFresh.Logo.png`, not `Amazon.Fresh.Logo.png`)
- File names should follow the general convention `{Key}[.{Modifier}][.{Width}x{Height}[.w{TargetWidth}][@{PixelDensity}x][.jpg|png|gif]`, where:
  - `{Key}` is the unique (base) identifier for the image (e.g., `Logo`)
  - `{Modifier}` is a modifier for content variations of an image (e.g., `StandAlone`, `Landscape`, `Portrait`, `FullScreen`, `Background`)
  - `{Width}` and `{Height}` represent the physical image dimensions (e.g., `500x250`); see note below
  - `{TargetWidth}` represents the *minimum* screen size this image should be used on (e.g., `500` represents 500px+ screens); this should be smaller than the image width
  - `{PixelDensity}` represents the minimum pixel density targeted by the image (e.g., `@1x`, `@1.5x`, `@2x`)
  - e.g., `Logo.StandAlone.w500.@2x.png`
- Target width and pixel density should only be included in a file name if multiple sizes of a file are provided
  - These values can be used by automated tools to generate CSS Media Queries of HTML5 `<picture>` elements
- Avoid encoding image dimensions into the file name *unless* multiple sizes may be used for the same screen size (e.g., a small logo and a large logo)
- For icons that represent particular content types and are not stored in a sprite, use the file extension for the key (e.g., `docx.16x16.png`, `pdf.16x16.png`)
  - Targets for these can be automated in CSS using, for instance, `src[~.docx]`

## Production Standards
- By convention, icons should be sized by multiples of 16x16 (e.g., 16x16, 32x32, 64x64, etc.)
- When including images in HTML, always specify the `alt` attribute; for layout "glyphs" this may be set to `*`
- Prefer removing metadata from images to reduce file size and, in some cases, preserve privacy
- Avoid placing text in images; this is difficult to maintain and localize, decentralizes styling, reduces accessibility, and increases page load
  - Prefer positioning text on top of images using CSS positioning or SVG compositions
  - If necessary, prefer compositing variable text into graphics dynamically using `<canvas>` or server-side components (e.g., [GDI+](https://msdn.microsoft.com/en-us/library/windows/desktop/ms533798%28v=vs.85%29.aspx), [ImageMagick](http://www.imagemagick.org/))
- Prefer providing one image file per graphic, based on the largest anticipated size requirement
  - Use multiple image files if the graphic:
    - Will vary based on dimensions (e.g., removing logotype on smaller screens), or
    - Requires fine production control (e.g., with transparent PNG-8 icons)
- Always compress images prior to production using an image processing tool (e.g., [TinyPNG](https://tinypng.com/))
  - This should ideally be automated as part of the build process (e.g., [gulp-imagemin](https://github.com/sindresorhus/gulp-imagemin))
- CSS sprites are recommended for commonly repeated UI elements, such as iconography and layout adornments (such as graphical backgrounds, borders, bullets, etc)
- For tiling images, smaller isn't necessarily better; a larger image may take more time to download, but less time to render

### Formats
- SVG should be used for vector-sourced content as it is scalable, generally smaller, and can be independently styled
- JPEG should be used primarily for photographs
  - JPEGs should target a quality level ~60, although this will need to vary by application
  - JPEGs should *not* be exported with a color profile; if a color profile exists, it should be converted to RGB
- PNG-8 (with 256 indexed colors) should be used for text or icons that contain a limited color palette are *not* anti-aliased
- PNG-24 (with full transparency) should be used for text, icons, or illustrations that require full transparency support
- GIF should be used *exclusively* for short animations (e.g., "spinners"), in cases where the animation cannot be accomplished via CSS; otherwise prefer PNG-8
