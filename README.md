<p align="center">
  <img src="images/logo.png" alt="DrewMark Logo">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Type-Specification-blue?style=flat-square" alt="Specification">
  <img src="https://img.shields.io/badge/Spec-v2.3-green?style=flat-square" alt="Spec v2.3">
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=flat-square" alt="MIT License">
  <img src="https://img.shields.io/badge/Lang-English%20%7C%20Chinese-red?style=flat-square" alt="Bilingual">
</p>

# DrewMark

A full-featured markup language system inspired by [Markdown](https://daringfireball.net/projects/markdown/) and [Showdown](https://github.com/showdownjs/showdown). DrewMark defines a set of standardized syntax rules for plain text content, easily parsed into standard HTML.

---

## Why DrewMark?

Markdown is great, but it has limitations. DrewMark rethinks the markup experience from the ground up:

- **9 text decorations** instead of just 2 — bold, italic, underline, strikethrough, highlight, superscript, subscript, small text, and ruby annotations
- **5 ordered list types** — Arabic numerals, Roman numerals (upper/lower), and Latin letters (upper/lower), with optional reverse ordering
- **3 unordered list types** — disc, circle, and square — each with distinct markers
- **Built-in table support** with `<thead>`, `<tbody>`, `<tfoot>`, colspan, and rowspan
- **Native multimedia embedding** — audio and video with codec selection, poster images, and playback controls
- **Citation support** for both inline quotes and blockquotes via the `cite` attribute
- **Global attribute system** — add `id`, `class`, `style`, `lang`, `align`, `dir`, `title`, and `data-*` to any element
- **Collapsible details blocks** with multi-level nesting
- **Progress bars**, **figure blocks**, **definition lists**, **style blocks**, and more
- **No ambiguous syntax** — curly braces for URLs, distinct markers for every decoration

---

## Quick Example

```drewmark
# Welcome to DrewMark

This is **bold**, this is %%italic%%, and this is !!highlighted!!.

## Task List
+*+ Implement parser
-*- Write documentation
+*+ Publish to npm

## Table
| Name     | Version |
| ======== | ======= |
| DrewMark | v2.3    |
```

---

## Project Structure

This repository contains the **DrewMark language specification** only. For implementations, see:

* [Javascript Parser](/drewneon/drewmark-js-parser)
* [Javascript Editor](/drewneon/drewmark-js-editor)
* [Javascript Converter](/drewneon/drewmark-js-converter)

---

## Documentation

Full language specification: [docs/doc.md](docs/doc.md)

中文文档: [docs/doc-cn.md](docs/doc-cn.md)

---

## License

MIT
