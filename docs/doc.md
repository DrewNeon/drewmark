<p align="center">
  <img src="../images/logo.png" alt="DrewMark Logo">
</p>

# DrewMark Documentation

## Table of Contents

1. [Project Introduction](#1-project-introduction)
2. [Syntax Overview](#2-syntax-overview)
3. [Tag Syntax Rules](#3-tag-syntax-rules)
4. [Attribute Syntax Rules](#4-attribute-syntax-rules)
5. [Escaping Rules](#5-escaping-rules)

---

## 1. Project Introduction

DrewMark is a full-featured markup language system inspired by [Markdown](https://daringfireball.net/projects/markdown/) and [Showdown](https://github.com/showdownjs/showdown). DrewMark uses a set of standardized syntax rules for plain text content, allowing it to be easily parsed into standard HTML code for displaying formatted content in web-supported scenarios, while avoiding risks or troubles caused by directly storing HTML code. For users familiar with Markdown, DrewMark syntax is easy to understand, but the differences are also very obvious. Identical syntax is marked as `(Same as Markdown)` in the corresponding section titles.

For security reasons, DrewMark does not include syntax for parsing form tags, except using `<input type="checkbox">` to show check status in "task lists", following Markdown's convention.

---

## 2. Syntax Overview

### 2.1 About Tags

HTML tags are mainly divided into two categories: block-level elements and inline elements. The main difference is whether they occupy the full width of the page. Therefore, block-level elements in a markup language should occupy one or more entire lines. Lines without any block-level marker are interpreted as paragraphs (`<p></p>`) by default. And based on how the lines are marked , block-level elements can be categorized into the following two types:
1. **Marked Per Line**: Specific marking rules **must** be applied to **each** line in this type of syntax. For instance, headings, lists, and blockquotes require respective markers at the beginning of each line, while the table syntax involves more complex marking conventions.
2. **Enclosed by Marker Lines**: This type of syntax **must** consists of multiple lines, with its scope defined by a starting marker line and an ending marker line. For example, the code block syntax is enclosed by two lines of ```` ``` ````.

Inline elements can be placed almost anywhere, usually enclosed by designated markers on both ends. 

The tree diagram below lists elements supported by DrewMark by categories, which is slightly different from the order in Chapter 3.

```
├── Block Elements
│   │
│   ├── Marked Per Line
│   │   │
│   │   ├── H 3.1 Headings
│   │   │
│   │   ├── 3.5 ☷ Lists
│   │   │   │
│   │   │   ├── 3.5.1 Unordered Lists
│   │   │   │   ├── ● Disc
│   │   │   │   ├── ○ Circle
│   │   │   │   └── ■ Square
│   │   │   │
│   │   │   ├── 3.5.2 Ordered Lists
│   │   │   │   ├── 1 Arabic numerals
│   │   │   │   ├── i Lowercase Roman numerals
│   │   │   │   ├── I Uppercase Roman numerals
│   │   │   │   ├── a Lowercase letters
│   │   │   │   └── A Uppercase letters
│   │   │   │
│   │   │   └── 3.5.3 Task Lists
│   │   │       ├── ☑ Done
│   │   │       └── ☐ Undone
│   │   │   
│   │   ├── ⊞ 3.6 Table
│   │   │
│   │   ├── ⧉ 3.7 Embeds
│   │   │   ├── 🔊 3.7.4 Audio
│   │   │   └── 🎬 3.7.5 Video
│   │   │
│   │   ├── ✎ 3.8.1 Definition List
│   │   │
│   │   ├── ❞ 3.9.2 Quote Block
│   │   │
│   │   └── — 3.11 Horizontal Rule
│   │ 
│   └── Enclsed by Marker Lines
│       │
│       ├── ■ 3.4.2 Code Block
│       │
│       ├── 🏞 3.7.3 Figure Block
│       │
│       ├── ▶ 3.8.2 Details Block
│       │
│       └── ✿ 3.12 Style Block
│ 
├── Inline Elements
│   │
│   ├── 3.2 Text Decors
│   │   ├── B Bold
│   │   ├── I Italic
│   │   ├── U Underline
│   │   ├── S Strikethrough
│   │   ├── ★ Highlight
│   │   ├── x² Superscript
│   │   ├── x₂ Subscript
│   │   ├── aA Small Font
│   │   └── /ɑ:/ Phonetic Transcription
│   │
│   ├── ☺ 3.3 Emoji
│   │
│   ├── </> 3.4.1 Inline Code
│   │
│   ├── 3.7 Embeds
│   │   ├── 🔗 3.7.1 Link
│   │   └── 🖼 3.7.2 Inline Image
│   │
│   ├── ❝ 3.9.1 Inline Quote
│   │
│   └── ◐ 3.10 Progress Bar
```

---

### 2.2 About Attributes

HTML tags use various attributes to set different parameters. Some attributes are global, meaning they can be used by literarily any tag, such as ` id=""`; some are specific, meaning they can only be used by one or a few tags, such as ` cite=""` for `<q>` and `<blockquote>` tags. Specific attributes are divided into optional and required. ` cite=""` is optional; without it, the basic functions of `<q>` and `<blockquote>` are not affected. The ` src=""` attribute is required for `<img>` tags; without it, `<img>` cannot display images.

DrewMark handles different types of attributes differently. Global attributes are explained separately in Section 2 of Chapter 4, and specific attributes are integrated into their corresponding tag syntax. Required attributes are important parts of tag syntax; without them, the corresponding tag syntax won't stand and cannot be parsed into the corresponding tag. Optional attributes are also integrated into the corresponding tag syntax, enclosed by `【】` for distinction.

## 3. Tag Syntax Rules

### 3.1 Headings (Same as Markdown)

| Syntax             | Description                                             | Parsed Output        |
| ------------------ | ------------------------------------------------------- | -------------------- |
| `# Heading 1`      | Line starting with one hash + at least one space        | `<h1>Heading 1</h1>` |
| `## Heading 2`     | Line starting with two hashes + at least one space      | `<h2>Heading 2</h2>` |
| `### Heading 3`    | Line starting with three hashes  + at least one space   | `<h3>Heading 3</h3>` |
| `#### Heading 4`   | Line starting with four hashes + at least one space     | `<h4>Heading 4</h4>` |
| `##### Heading 5`  | Line starting with five hashes + at least one space     | `<h5>Heading 5</h5>` |
| `###### Heading 6` | Line starting with six hashes + at least one space      | `<h6>Heading 6</h6>` |

---

### 3.2 Text Decors

Markdown only has a few text emphasis syntaxes, among which the enclosing markers of bold and italic can be confusing. The redesigned syntax in DrewMark not only avoids any possible confusion but also greatly expands, making full use of HTML tags to decorate texts.

| Syntax              | Description                                            | Parsed Output                        | 
| ------------------- | ------------------------------------------------------ | ------------------------------------ |
| `**Bold**`          | Content enclosed by double asterisks                   | `<strong>Bold</strong>`              |
| `%%Italic%%`        | Content enclosed by double percent signs               | `<em>Italic</em>`                    |
| `~~Strikethrough~~` | Content enclosed by double tildes                      | `<del>Strikethrough</del>`           |
| `__Underline__`     | Content enclosed by double underscores                 | `<ins>Underline</ins>`               |
| `!!Highlight!!`     | Content enclosed by double exclamation marks           | `<mark>Highlight</mark>`             |
| `^^Superscript^^`   | Content enclosed by double carets                      | `<sup>Superscript</sup>`             |
| `<<Subscript>>`     | Content enclosed by double angle brackets              | `<sub>Subscript</sub>`               |
| `@@Small Font@@`    | Content enclosed by double at signs                    | `<small>Small Font</small>`          |
| `{{Text^Phonetic}}` | Content enclosed by double braces and split by a caret | `<ruby>Text<rt>Phonetic</rt></ruby>` |

Note: All syntaxes in this section can be combined and nested. For example, `**%%Bold + Italic%%**` is parsed as `<strong><em>Bold + Italic</em></strong>`.
 
 ---

### 3.3 Emoji

**Syntax**: `::emoji_name::`

**Details**: A string enclosed by double colons that matches an emoji name.

**Example**: `::smile::` → 😄, `::heart::` → ❤️

### 3.4 Code (Same as Markdown)

#### 3.4.1 Inline Code

**Syntax**: `` `Code` ``

**Details**: Content enclosed by an equal number of backticks.

**Parsed Output**: `<code>Code</code>`

#### 3.4.2 Code Blocks

**Syntax**:
````
```【Code Lang】
Code content
```
````
**Details**: Multi-line content enclosed by two lines, each starting with at least three consecutive backticks of equal number. The opening marker line supports an optional code language identifier immediately after ```` ``` ````.

**Parsed Output**:
```
<pre>
  <code>
    Code content
  </code>
</pre>
```

---

### 3.5 Lists

#### 3.5.1 Unordered Lists

Although Markdown's unordered lists support three types of leading markers: the plus sign (`+`), the minus sign (`-`), and the asterisk (`*`), they are all uniformly rendered as `<ul>` tags without any type attribute. DrewMark makes a clear distinction: different leading markers correspond to different `type` values for the `<ul>` tag.

| Syntax     | Description                                       | Parsed Output                            |
| ---------- | ------------------------------------------------- | ---------------------------------------- |
| `+ Disc`   | Lines starting with plus + at least one space     | `<ul type="disc"><li>Disc</li></ul>`     |
| `- Circle` | Lines starting with minus + at least one space    | `<ul type="circle"><li>Circle</li></ul>` |
| `* Square` | Lines starting with asterisk + at least one space | `<ul type="square"><li>Square</li></ul>` |

---

#### 3.5.2 Ordered Lists

Markdown only supports one type of ordered list syntax, i.e. lines started with an arabic number + `.`, corresponding to the `<ol>` tag without `type` attribute; while DrewMark extends to all the five different `type` values of the `<ol>` tag.

| Syntax                 | Description                                       | Parsed Output                                                |
| ---------------------- | -------------------------------------------------- | ----------------------------------------------------------- |
| `【!】1. Arabic`       | Lines starting with any number + dot + space       | `<ol【 reversed】><li>Arabic</li></ol>` (default `type="1"`) |
| `【!】i. Lower Roman`  | Lines starting with lowercase Roman + dot + space  | `<ol type="i"【 reversed】><li>Lower Roman</li></ol>`        |
| `【!】I. Upper Roman`  | Lines starting with uppercase Roman + dot + space  | `<ol type="I"【 reversed】><li>Upper Roman</li></ol>`        |
| `【!】a. Lower Letter` | Lines starting with lowercase letter + dot + space | `<ol type="a"【 reversed】><li>Lower Letter</li></ol>`       |
| `【!】A. Upper Letter` | Lines starting with uppercase letter + dot + space | `<ol type="A"【 reversed】><li>Upper Letter</li></ol>`       |

Notes:
1. The starting number of the first line determines the start number of the list. For example, a list starting with `2. First line` is parsed as `<ol start="2"><li>First line</li></ol>`. Subsequent lines only need to match the number format; the actual number written does not matter.
2. Ordered lists can be reversed by adding an exclaimation mark at the start of the first line.

#### 3.5.3 Task Lists

DrewMark follows Markdown convention and provides two task list types.

There is no direct "task list" tag in HTML. It is implemented by hiding default list styles with CSS and using `<input type="checkbox">` to show the task status. DrewMark treats task lists as special unordered lists, hence using combinations of unordered list markers.

| Syntax       | Description                                          | Parsed Output                                                                            | 
| ------------ | ---------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `+*+ Done`   | Lines starting with plus + asterisk + plus + space   | `<ul class="task-list"><li><input type="checkbox" checked="" disabled="">Done</li></ul>` |
| `-*- Undone` | Lines starting with minus + asterisk + minus + space | `<ul class="task-list"><li><input type="checkbox" disabled="">Undone</li></ul>`          |

Note: a `class="task-list"` attribute is added to the `<ul>` tag in order to easily override the browser's default styles for `<ul>` elements via CSS.

#### 3.5.4 Multi-level Nesting

Consecutive lines with the same leading marker type are parsed into the same `<ul>` or `<ol>`. Like Markdown, DrewMark supports multi-level nesting based on indentation spaces before the leading markers.

**DrewMark**:
```
1. First batch status
    +*+ Item 1
    -*- Item 2
2. Second batch status
    +*+ Item 1
    -*- Item 2
```
**Parsed Output**:
```html
<ol>
    <li>First batch status
        <ul class="task-list">
            <li><input type="checkbox" checked="" disabled=""> Item 1</li>
            <li><input type="checkbox" disabled=""> Item 2</li>
        </ul>
    </li>
    <li>Second batch status
        <ul class="task-list">
            <li><input type="checkbox" checked="" disabled=""> Item 1</li>
            <li><input type="checkbox" disabled=""> Item 2</li>
        </ul>
    </li>
</ol>
```

---

### 3.6 Table

**Syntax**:
```
| Header 1 | Header 2 |
| ==== | ==== |
| Row1 Col1 | Row1 Col2 |
| ==== | ==== |
| Footer 1 | Footer 2 |
```

**Details**:
1. A line starting and ending with | (spaces allowed) is recognized as a table row.
2. A line in the format `|====|` is a structural divider line, separating `<thead>`, `<tbody>`, `<tfoot>`.
3. Structural lines only divide structure; texts within those lines are discarded during parsing.
4. Rules for structural lines:
  - *one* structural line only: no `<tfoot>`; lines before the structual line belong to `<thead>`, while those after to `<tbody>`.
  - *no less than two* structural lines: only the first and last are valid; lines between those structural lines belong to `<tbody>`, lines before the first to `<thead>`, while those after the last to `<tfoot>`.
  - *No* structural lines: all content lines belong to `<tbody>`.
5. `<thead>`, `<tbody>`, `<tfoot>` all supports any number of rows.

**Parsed Output**:
```html
<table>
  <thead>
    <tr>
      <th>Header 1</th>
      <th>Header 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Row1 Col1</td>
      <td>Row1 Col2</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Footer 1</td>
      <td>Footer 2</td>
    </tr>
  </tfoot>
</table>
```

**Cell Colspan & Rowspan**
| Syntax       | Description                                                                          | Parsed Output       |
| ------------ | ------------------------------------------------------------------------------------ | ------------------- |
| `&<number>&` | ampersand + left angle bracket + positive integer + right angle bracket + ampersand  | ` colspan="number"` |
| `&/number/&` | ampersand + slash + positive integer + slash + ampersand                             | ` rowspan="number"` |

Note: Colspan and rowspan must be inside cells (enclosed by `|`) and do not work in structural lines.

Colspan example: 
```
| Header 1 | Header 2 |
| ==== | ==== |
| Row1 Col1 &<2>& |
| Row2 Col1 | Row2 Col2 |
```
→
```
<table>
  <thead>
    <tr>
      <th>Header 1</th>
      <th>Header 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2">Row1 Col1</td>
    </tr>
    <tr>
      <td>Row2 Col1</td>
      <td>Row2 Col2</td>
    </tr>
  </tbody>
</table>
```

Rowspan example: 
```
| Header 1 | Header 2 |
| ==== | ==== |
| Row1 Col1 &/2/& | Row1 Col2 |
| Row2 Col1 |
```
→
```html
<table>
  <thead>
    <tr>
      <th>Header 1</th>
      <th>Header 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Row1 Col1</td>
      <td>Row1 Col2</td>
    </tr>
    <tr>
      <td>Row2 Col1</td>
    </tr>
  </tbody>
</table>
```

---

### 3.7 Embedding

HTML itself is a plain-text file and does not contain multimedia content, but it can be embedded into pages through specific tags. The syntaxes in this chapter are for these tpye of tags.

#### 3.7.1 Link

**Syntax**: `(【display text】){URL【=>target】}`

**Details**:
1. Starts with a pair of parentheses, which can optionally contain display text (if omitted, the URL itself is displayed directly), immediately followed by a URL enclosed by curly braces. After the URL, you can append the link target using `=>` as the separator.
2. The "target" refers to the `target=` attribute of the HTML `<a>` tag. If omitted, the default is the current window (`_self`). Accepted values and their meanings are shown in the table below; values other than these will be discarded along with the separator.
3. Spaces prior to the separator `=>` are allowed to separate the target from the URL, but no spaces are allowed after the separater.

| Accepted Value    | Meaning        | Shortcut (case-insensitive) |
| ----------------- | -------------- | ----------------------------|
| `_self` (default) | Current window | `self` or `s`               |
| `_blank`          | New window     | `blank` or `b`              |
| `_parent`         | Parent window  | `parent` or `p`             |
| `_top`            | Full window    | `top` or `t`                |

**Parsing Examples**:
| DrewMark Text                           | Parsed Output                                                  |
| --------------------------------------- | -------------------------------------------------------------- |
| `(Click here){https://example.com}`     | `<a href="https://example.com">Click here</a>`                 |
| `(){https://example.com}`               | `<a href="https://example.com">https://example.com</a>`        |
| `(Click here){https://example.com =>b}` | `<a href="https://example.com" target="_blank">Click here</a>` |

Note: This looks similar to Markdown’s link syntax yet completely different. DrewMark’s modification is not intend to merely differentiate itself from Markdown, but to more easily avoid misjudging special cases. Markdown’s link syntax uses parentheses `()` to wrap URLs, yet according to RFC 3986, parentheses are valid characters, i.e. URLs ending with `)` may exist. If the parser ignores this possibility, some specical URLs may become inaccessible due to a missing closing `)`. While this is not technically difficult to fix, preventing this problem fundamentally is even better. Among the three types of parentheses, which are the most intuitive enclosing symbols, only curly braces are invalid in URLs. Although modern browsers can accept URLs containing curly braces, RFC 3986-compliant URLs are the vast majority. Therefore, DrewMark uses curly braces exclusively to wrap URLs in all the syntaxes. The part before curly braces is changed to parentheses because DrewMark uses square brackets for attribute syntaxes.

#### 3.7.2 Inline Image

**Syntax**: `!(【alt text】【/width|height/】){image URL}`

**Details**: Starts with an exclamation mark and a pair of parentheses, optionally containing alt text (omit it if no `alt=` attribute needed) and dimension part (`/|/`) (see table below); immediately followed by an image URL enclosed by curly braces.

| Format                 | Meaning                                      | Parsed Output                        |
| ---------------------- | -------------------------------------------- |------------------------------------- |
| `/integer1\|integer2/` | Set width to integer1 and height to integer2 | `width="integer1" height="integer2"` |
| `/integer/`            | Set width to integer only                    | `width="integer"`                    |
| `/\|integer/`          | Set height to integer only                   | `height="integer"`                   |
| Omit `/\|/` part       | Use original image size                      | None                                 |

Note: Width and height is independent. If either value is not a positive integer, the corresponding attribute is not output. For example, `/abc|200/` outputs `height="200"` only; while `/200|6.2/` outputs `width="200"` only.

**Full Example**:
| DrewMark Text                                       | Parsed Output                                                                  |
| --------------------------------------------------- | ------------------------------------------------------------------------------ |
| `!(Logo /50\|50/){https://example.com/logo.png}`    | `<img src="https://example.com/logo.png" alt="Logo" width="50" height="50" />` |
| `!(Thumbnail /200/){https://example.com/image.png}` | `<img src="https://example.com/image.png" alt="Thumbnail" width="200" />`      |
| `!(){https://example.com/image.png}`                | `<img src="https://example.com/image.png" />`                                  |

#### 3.7.3 Figure Block

**Syntax**:
```
【! Image caption】
!(【alt text】【/width|height/】){image URL}
【! Image caption】
!(【alt text】【/width|height/】){image URL}
```

**Description**: Multi-line content enclosed by two lines starting with at least three consecutive exclamation marks. Lines starting with `! ` (exclamation mark + space) are parsed as image captions (`<figcaption>`). Caption lines support text-decoration syntaxes. Lines containing inline-image syntax are stripped of extra texts and output the parsed image tag only. Lines that match neither are discarded (no output).

**Parsed Output**:
```html
<figure>
  【<figcaption>Image caption</figcaption>】
   <img src="...">
   <figcaption>Image caption</figcaption>】
   <img src="...">
</figure>
```

---

#### 3.7.4 Audio

**Syntax**: `~(【_】【&】【@】【!】){URL1|Media Type}【{URL2|Media Type}】`

**Description**: A line starting with a tilde followed by a pair of parentheses, optionally containing additional attributes (see Table 1 below), immediately followed by a pair of curly braces containing a URL and a media type (see Table 2 below for supported types) seperated by a pipe sign. Multiple sets of curly braces can be used to append URLs of different media types. It should be specifically noted that although the `<audio>` tag is defined as an inline element in HTML, it is rarely mixed within a paragraph of text in practice. Therefore, DrewMark treats it as a block-level element, i.e. each audio syntax **must** occupy an entire line. Furthermore, if a line starts with valid audio syntax, any redundant textx on that line outside of the audio syntax will be discarded.

Table 1: Additional Attributes
| Symbol | Name             | Corresponding Attribute | Default Value |
| ------ | ---------------- | ----------------------- | ------------- |
| `_`    | Underscore       | ` controls`             | `true`        |
| `&`    | Ampersand        | ` autoplay`             | `false`       |
| `@`    | At Sign          | ` loop`                 | `false`       |
| `!`    | Exclamation Mark | ` muted`                | `false`       |

Notes:
1. Among the attributes listed in the table above, only `controls` has a different default value. The `controls` attribute is output by default; use the underscore sign only if you require it **not** to be output. The other three attributes are not output by default and will only be parsed and output if their corresponding symbol is used.
2. There is no requirement for the order of dimension specification and these four attributes, and spaces between parts are optional.

Table 2: Media Types
| Supported Media Type | Corresponding Value (Case Insensitive) | Parsed Output        |
| -------------------- | -------------------------------------- | -------------------- |
| MP3                  | `mp3` or `mpeg`                        | ` type="audio/mpeg"` |
| WAV (PCM)            | `wav` or `wave`                        | ` type="audio/wav"`  |
| OGG (Vorbis/Opus)    | `ogg`                                  | ` type="audio/ogg"`  |
| AAC                  | `aac`                                  | ` type="audio/aac"`  |
| FLAC                 | `flac`                                 | ` type="audio/flac"` |
| WebM                 | `webm`                                 | ` type="audio/webm"` |

Note: If a supported media type is not correctly specified, the corresponding `{URL|Media Type}` set is considered invalid and will **not** be parsed or output. If none of the sets contain a correctly specified media type, the syntax will fail to parse into an `<audio>` tag, but `~<a href="...">...</a>` instead, due to the syntax after the tilde conforms entirely to the link syntax.

**Complete Examples**

Example 1 (Most Concise): `~(){https://example.com/music/audio1|mp3}` is parsed to:
```html
<audio controls>
  <source src="https://example.com/music/audio1" type="audio/mpeg">
  Your browser does not support the audio tag.
</audio>
```

Example 2 (More Comprehensive): `~(&@){https://example.com/music/audio1|mp3}{https://example.com/music/audio2|ogg}` is parsed to:
```html
<audio controls autoplay loop>
  <source src="https://example.com/music/audio1" type="audio/mpeg">
  <source src="https://example.com/music/audio2" type="audio/ogg">
  Your browser does not support the audio tag.
</audio>
```

Note: "Your browser does not support the audio tag." is the standard fallback text for the `<audio>` tag.

---

#### 3.7.5 Video

**Syntax**: `$(【{Poster_Image_URL}】【/Specified_Width|Specified_Height/】【_】【&】【@】【!】){URL1|Media_Type}【{URL2|Media_Type}】`

**Description**: A line starts with a dollar sign followed by a pair of parentheses,optionally containing a poster image URL enclosed by curly braces, specified width and height (using the same method as in the image syntax), and additional attributes (refer to Table 1 and related notes in the audio syntax); immediately followed by a pair of curly braces containing a URL and a media type (see the table below for supported types) seperated by a pipe sign. Multiple sets of curly braces can be used to append URLs of different media types. It is important to note that although the `<video>` tag is defined as an inline element in HTML, it is rarely mixed within a paragraph of text in practice. Therefore, DrewMark treats it as a block-level element, i.e. each video syntax **must** occupy an entire line. Furthermore, if a line starts with valid video syntax, any redundant textx on that line outside of the video syntax will be discarded.

Table: Media Types
| Supported Media Type | Corresponding Value (Case-Insensitive) | Parsed Output        |
| -------------------- | -------------------------------------- | -------------------- |
| MP4                  | `mp4` or `mpeg`                        | ` type="video/mp4"`  |
| WebM                 | `webm`                                 | ` type="video/webm"` |
| OGG (Vorbis/Opus)    | `ogg`                                  | ` type="video/ogg"`  |
| AV1                  | `av1`                                  | ` type="video/av1"`  |
| MOV                  | `mov`                                  | ` type="video/mov"`  |

Note: If a supported media type is not correctly specified, the corresponding `{URL|Media_Type}` set is considered invalid and will **not** be parsed or output. If none of the sets contain a correctly specified media type, the content cannot be parsed into a `<video>` tag, but `$<a href="...">...</a>` instead, due to the syntax after the dollar sign conforms entirely to the link syntax.

**Complete Examples**

Example 1 (Most Concise): `$(){https://example.com/video/clip1|mp4}` is parsed to:
```html
<video controls>
  <source src="https://example.com/video/clip1" type="video/mp4">
  Your browser does not support the video tag.
</video>
```

Example 2 (More Comprehensive): `$({https://example.com/video/poster.jpg}/400|300/&@){https://example.com/video/clip1|mp4}{https://example.com/video/clip2|webm}` is parsed to:
```html
<video poster="https://example.com/video/poster.jpg" width="400" height="300" controls autoplay loop>
  <source src="https://example.com/video/clip1" type="video/mpeg">
  <source src="https://example.com/video/clip2" type="video/webm">
  Your browser does not support the video tag.
</video>
```

Note: "Your browser does not support the video tag." is the standard fallback text for the `<video>` tag.

---

### 3.8 Description

This group contains two distinct tags used for definitions or descriptions.

#### 3.8.1 Definition List

**Syntax**: `;;Term::Description;;`

**Description**: A full line starting and ending with double semicolons, within which the term and the description are separated by a double colon.

**Parsed Output**:
```html
<dl>
  <dt>Term</dt>
  <dd>Description</dd>
</dl>
```

Note: Multiple lines of definition list syntax without intervals (including blank lines) will be parsed into a single `<dl>` tag. For example:
```
;;Term1:: Description1;;
;;Term2:: Description2;;
```
is parsed to:
```html
<dl>
  <dt>Term1</dt>
  <dd>Description1</dd>
  <dt>Term2</dt>
  <dd>Description2</dd>
</dl>
```

---

#### 3.8.2 Details Block

**Syntax**:
```
;;;【Title】
Multi-syntax content
;;;【>】
```

**Description**: Multi-line content enclosed by two lines that each starts with at least three consecutive semicolons. A title may optionally follow the `;;;` on the opening marker line (if omitted, different browsers will supply their own default text). A right angle bracket sign may be appended after the `;;;` on the closing marker line to indicate that the `<details>` tag shall be expanded by default when the page is loaded (the default state is collapsed, showing only the title or the browser's default text). Due to its syntactic structure, the details block is the only tag capable of containing all other tags; its content section supports not only any inline syntax but also any block-level syntax, all of which will be parsed normally.

**Parsed Output**

```html
<details【 open】>
  【<summary>Title</summary>】
  <p>Multi-syntax content</p>
</details>
```

**Multi-level Nesting**

Details blocks support multi-level nesting. Different nesting levels are represented similarly to nested lists, i.e. determined by the number of leading spaces at the beginning of each line. For example:

```
;;; Level 1 Title
Level 1 Content
  ;;; Level 2 Title
  Level 2 Content
  ;;;>
;;;
```
is parsed to:
```html
<details>
  <summary>Level 1 Title</summary>
  <p>Level 1 Content</p>
  <details open>
    <summary>Level 2 Title</summary>
    <p>Level 2 Content</p>
  </details>
</details>
```

---

### 3.9 Quotes

#### 3.9.1 Inline Quote

**Syntax**: `>>Quote Text【{<=URL}】<<`

**Description**: Content enclosed by double right angle brackets and double left angle brackets. It supports an optional citation source enclosed by curly braces after the quote text, i.e. the `{<=URL}` part.

**Parsed Output**: `<q【 cite="URL"】>Quote Text</q>`

#### 3.9.2 Quote Block

**Syntax**: `> Quote Content【{<=URL}】`

**Description**: A line starting with one or more consecutive right angle brackets (where the count indicates the nesting level) followed by at least one space. It supports an optional citation source enclosed by curly braces (same as inline quotations). Each nesting level supports only one citation source, which must be placed at the end of the last line of that level. Consecutive lines of content at the same level are parsed into a single `<p>` paragraph, each line separated by `<br>`. To split multiple `<p>` paragraphs within the same level, you must insert an empty line at the same level between them, i.e. a line starting with a matching number of right angle brackets followed by at least one space.

**Parsed Output**: `<blockquote【 cite="URL"】><p>Quote Content</p></blockquote>`

**Multi-level Multi-line Example**:

DrewMark:
```
> Level 1 Quote
>> Level 2 Quote Line 1
>> Level 2 Quote Line 2【{<=URL}】
>>> Level 3 Quote Paragraph 1
>>> 
>>> Level 3 Quote Paragraph 2
```

Parsed Output:
```html
<blockquote>
  <p>Level 1 Quote</p>
  <blockquote【 cite="URL"】>
    <p>Level 2 Quote Line 1<br>Level 2 Quote Line 2</p>
    <blockquote>
      <p>Level 3 Quote Paragraph 1</p>
      <p>Level 3 Quote Paragraph 2</p>
    </blockquote>
  </blockquote>
</blockquote>
```

**Containing Block-level Elements**: Since a quote block is a single-line block-level element, i.e. its block nature is determined by the marker at the beginning of each line, it can contain not only plain paragraphs or inline syntax but also other single-line block-level elements such as lists, audio, video, and definition lists. For example:
```
> 1. Item One
> A. Item A
> ~(){https://example.com/music/audio1|mp3}
>  $ (){https://example.com/video/clip1|mp4}
> ;;Term::Definition;;
```
is parsed to:
```html
<blockquote>
  <ol><li>Item One</li></ol>
  <ol type="A"><li>Item A</li></ol>
  <audio controls>
    <source src="https://example.com/music/audio1" type="audio/mpeg">
    Your browser does not support the audio tag.
  </audio>
  <video controls>
    <source src="https://example.com/video/clip1" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <dl><dt>Term</dt><dd>Definition</dd></dl>
</blockquote>
```

---

### 3.10 Progress Bar

**Syntax**: `((value//【max】))`

**Description**: Content enclosed by two sets of parentheses, which must be divided into two parts by a double slash, and both parts must be positive number. The "max" part is optional and defaults to `1`.

**Parsed Output**: `<progress value="value" max="max"></progress>`

---

### 3.11 Horizontal Rule (Same as Markdown)

**Syntax**: `---`

**Description**: A line starting with at least three consecutive hyphens; any content following them will be discarded.

**Parsed Output**: `<hr>`

---

### 3.12 Style Block

**Syntax**:
```
{{{【media】
  Multi-line CSS code
}}}
```

**Description**: Multi-line content enclosed by a line starting with at least three left curly braces and a line starting with at least three right curly braces. The opening marker line optionally supports the value of the `meida` attribute immediately after `{{{`.

**Parsed Output**:
```html
<style【 media="media"】>
  Multi-line CSS code
</style>
```

---

## 4. Attribute Syntax Rules

### 4.1 Summary of Dedicated Attributes

Dedicated attributes are tightly bound to the syntaxes of their respective tag via format requirements and even placement rules. The following table summarizes all dedicated attributes; for their detailed usage, please refer to the corresponding tag syntax rules.

| Attribute       | Syntax                  | Output                                   | Applicable Tags           |
| --------------- | ----------------------- | ---------------------------------------- | ------------------------- |
| Reverse Order   | `!`                     | ` reversed`                              | Ordered Lists             |
| Column Span     | `&<positive integer>&`  | ` colspan="positive integer"`            | Table's Data Cells        |
| Row Span        | `&/positive integer/&`  | ` rowspan="positive integer"`            | Table's Data Cells        |
| Target          | `=>target window`       | ` target="target window"`                | Link                      |
| Dimensions      | `/pos int1\|pos int2/`  | ` width="pos int1" height="pos int2"`    | Image, Video              |
| Controls, etc.  | `_`/`&`/`@`/`! `        | ` controls`/` autoplay`/` loop`/` muted` | Audio, Video              |
| Poster Image    | `{URL}`                 | ` poster="URL"`                          | Video                     |
| Citation Source | `<=URL`                 | ` cite="URL"`                            | Quotes (Inline & Block)   |
| Expanded        | `>`                     | ` open`                                  | Details Blocks            |
| Media type      | {{{`meida type`         | ` media="media type"`                    | Style Blocks              |

---

### 4.2 Global Attributes

#### 4.2.1 Syntax Rules

Global attributes, as the name suggests, are applicable to almost all tags. Therefore, unlike dedicated attributes that are deeply bound to the syntax of their specific elements, global attributes follow a unified syntax rule instead.

**Syntax**: `[AttrAbbr[ AttrValue ]【AttrAbbr】]`

**Description**: Left square bracket + attribute abbreviation letter + left square bracket + *attribute value* + right square bracket + 【attribute abbreviation letter】 + right square bracket. The "attribute abbreviation letter" is case-insensitive, and the second occurrence is optional. Spaces are allowed around the attribute value, but **not** in any other part. The detailed rules for various global attributes are listed in the table below:

| Attribu te       | Syntax                                 | Accepted Values                                                                  | Output                                     |
| ---------------- | -------------------------------------- | -------------------------------------------------------------------------------- | ------------------------------------------ |
| Horizontal Align | `[A[ Accepted Value ]A]`               | `left` (default), `center`, or `right`                                           | ` align="Accepted Value"`                  |
| Class            | `[C[ Class Name ]C]`                   | String composed of letters, digits, `-`, `_`, and spaces                         | ` class="Class Name"`                      |
| Text Direction   | `[D[ Accepted Value ]D]`               | `ltr` (default), `rtl`, or `auto`                                                | ` dir="Accepted Value"`                    |
| ID               | `[I[ ID Name ]I]`                      | String composed of letters, digits, `-`, `_`, `:`, `.`, must start with a letter | ` id="Accepted Value"`                     | 
| Language         | `[L[ Lang Name ]L]`                    | BCP 47 language code                                                             | ` lang="Lang Name"`                        |
| Style            | `[S[ CSS ]S]`                          | CSS style format                                                                 | ` style="Style"`                           |
| Title            | `[T[ Title Text ]T]`                   | Any characters except `<`, `>`, `&`, `"`                                         | ` title="Title Text"`                      |
| data-*           | `[-[ Key:Value【, Key2:Value2】...]-]` | Same as above                                                                    | ` data-key="Value"【 data-key2="Value2"】` |

---

#### 4.2.2 Position and Attribution

Every tag syntax has a defined scope, which is either the content enclosed between opening and closing markers or an entire line that conforms to the syntactic rules. In most cases, global attributes can be placed anywhere within the scope of a given tag syntax, but there are also scenarios with stricter requirements.

+ **Completely Unsupported**:
  - *Emoji*: The parsed result of emoji syntax is merely a symbol and does not contain any HTML tags. Therefore, global attributes written inside emoji syntax will not only be output as-is but also prevent the correct emoji from being matched. Thus, do not write any global attributes within the scope of emoji syntax!
  - *Inline Code*: The `<code>` tag is used to present raw code, so global attributes written within inline code scope will also be output as-is.

+ **Must Be Placed in Fixed Positions**:
  - *Code Blocks*: Content lines within code blocks behave the same as inline code, i.e. all content (including global attribute syntax) is output as-is. However, as a multi-line block-level element, the opening marker line of a code block supports global attribute in addition to the programming language specified.
  - *Style Blocks*: Style blocks are structured similarly to code blocks, and their opening marker lines likewise support global attributes.
  - *Progress Bar*: Since the `<progress>` tag displays the percentage relationship between `value` and `max` graphically, the corresponding two parts in its syntax must be positive number. Therefore, attributes in progress bar syntax must be written inside the delimiter `//`, e.g., `((32/[C[ green ]C]/46))`, so that it can be parsed to `<progress class="green" value="32" max="46"></progress>`.
  - *The Embed Group*: Except for figure blocks, the four syntaxes of the embed group (namely links, images, audio, and video) share a basic structure, i.e. `()` + `{}`. The curly brace part is mainly used for the embedded URL, while various dedicated attributes are written in the parenthesis part. Obviously, global attributes must also be written within `()`.
  - *Horizontal Rules*: Although most global attributes are meaningless for horizontal rules, according to the HTML specification, the `<hr>` tag does support global attributes. Therefore, DrewMark also supports global attributes written after the consecutive hyphens.

+ **Different Positions Correspond to Different Tags**:
  - *Ruby Annotations*: `{{Global attributes here belong to the <ruby> tag^Global attributes here belong to the <rt> tag}}`
  - *Definition Lists*: `;;Global attributes here belong to the <dt> tag::Global attributes here belong to the <dd> tag;;Global attributes here belong to the <dl> tag`. For example: `;;Term [C[ dt-class ]C]::Definition [C[ dd-class ]C];; [C[ dl-class ]C]` is parsed to `<dl class="dl-class"><dt class="dt-class">Term</dt><dd class="dd-class">Definition</dd></dl>`.
  - *Figure Blocks*:
    ```
    !!!Global attributes here belong to the <figure> tag
      !Global attributes here belong to the <figcaption> tag
      Global attributes for image syntax must be written within `()`
    !!!
    ```
  - *Details Blocks*:
    ```
    ;;;Global attributes here belong to the <summary> tag
      Global attributes in lines without any block-level element syntax belong to the <p> tag
    ;;;
    ```
  - *Table*: Due to its complex structure, please refer to the relevant section in "Parent Tag Attributes" for details.

When there are mutilple nested layers of tag syntaxes, global attributes belong to the innermost tag according to their position. For example, the following three cases all consist of three layers of tags, namely `<h1>` → `<strong>` → `<mark>` from outside to inside, however, the global attribute belongs to different tags due to its specific postion.

| DrewMark                                                 | The location of the global attribute | The tag it belongs to | Parsed result                                         |
| -------------------------------------------------------- | ------------------------------------ | --------------------- | ----------------------------------------------------- |
| `# This is an **!!important[C[ important ]]!!** heading` | Within `!! !!`                       | `<mark>`              | `<h1>This is an <strong><mark class="important">important </mark></strong>heading</h1>` |
| `# This is am **!!important!![C[ important ]]** heading` | Within `** **`                       | `<strong>`            | `<h1>This is an <strong class="important"><mark>important </mark></strong>heading</h1>` |
| `# This is an **!!important!!** heading[C[ important ]]` | Within the line started with `# `    | `<h1>`                | `<h1 class="important">This is an <strong><mark>important </mark></strong>heading</h1>` |

---

#### 4.2.3 Special Cases

* *Non-standard Attribute*: When there is the language attribute (`([L[ en-US ]L]`) within the link syntax's `()`, the attribute name is **not** `lang`, but `hreflang` instead (`<a href="..." hreflang="en-US">...`).

---

### 4.3 Parent Tag Attributes

Some block-level elements contain multi-layer tag structures. According to the innermost principle, global attributes belong to the innermost tag corresponding to their position. To add attributes to tags at different layers, parent tag attributes are sometimes required. Except for the tag syntaxes specified below, others do not support parent tag syntax, i.e. any parent tag attributes written within them are discarded and will **not** add any attribute to any tag.

**Syntax**: `[AttrAbbr< AttrValue >【AttrAbbr】]`. 

**Description**: In short, just replace the inner layer of double square brackets in the standard attribute syntax with a pair of angle brackets; the rest remains consistent with the standard attribute syntax.

#### 4.3.1 Code Blocks

The HTML structure of a code block consists of two layers: `<pre>` → `<code>`. Since all text in a code block is output verbatim, including any DremMark syntax, attribute syntax must be written in the opening marker line. Standard attributes belong to `<code>`, while parent tag attributes are promoted to `<pre>`. For example:

**Standard Attribute**:
````
``` language [C[ code_class ]C]
Code
```
````
→ `<pre><code class="code_class">Code</code></pre>`。
**Parent Tag Attribute**:
````
``` language [C< pre_class >C]
Code
```
````
→ `<pre class="pre_class"><code>Code</code></pre>`。

---

#### 4.3.2 Lists

The HTML structure of a list consists of two layers: `<ul>`/`<ol>` → `<li>`. Standard attributes belong to `<li>`, while parent tag attributes are promoted to `<ul>`/`<ol>`. For example:

**Standard Attribute**: `1. Item One[A[ center ]A]` → `<ol><li align="center">Item One</li></ol>`. Effect: Only "Item One" is centered.

**Parent Tag Attribute**: `1. Item One[A< center >A]` → `<ol align="center"><li>Item One</li></ol>`. Effect: The entire ordered list is centered.

---

#### 4.3.3 Quote Block

The HTML structure of a quote block consists of two layers: `<blockquote>` and `<p>`. Standard attributes belong to `<p>`, while parent tag attributes are promoted to `<blockquote>`. For example:

**Standard Attribute**: `> First Paragraph [A[ center ]A]` → `<blockquote><p align="center">First Paragraph</p></blockquote>`. Effect: Only this paragraph is centered.

**Parent Tag Attribute**: `> First Paragraph [A< center >A]` → `<blockquote align="center"><p>First Paragraph</p></blockquote>`. Effect: The entire block quotation is centered.

---

#### 4.3.4 Details Block

The HTML structure of a details block consists of two layers: `<details>` and `<summary>`/`<p>`. Standard attributes belong to the corresponding `<summary>` or `<p>` based on their position, while parent tag attributes are promoted to `<details>`. For example:

**Standard Attribute**:
```
;;; Title [A[ center ]A]
Content
;;;
```
→ `<details><summary align="center">Title</summary><p>Content</p></details>`. Effect: Only the "Title" part is centered.
```
;;; Title
Content [A[ center ]A]
;;;
```
→ `<details><summary>Title</summary><p align="center">Content</p></details>`. Effect: Only the "Content" part is centered.

**Parent Tag Attribute**:
```
;;; Title [A< center >A]
Content
;;;
```
or
```
;;; Title
Content [A< center >A]
;;;
```
→ `<details align="center"><summary>Title</summary><p>Content</p></details>`. Effect: The entire details block is centered.

---

#### 4.3.5 Tables

The HTML structure of tables is the most complicated, consisting of four layers in total:
1. `<table>`
2. `<thead>`/`<tbody>`/`<tfoot>`
3. `<tr>`
4. `<th>`/`<td>`
The attribution to which level of tags depends on the different positions of standard attributes and parent tag attributes.

**Standard Attributes**:
1. Attributes within content row cells belong to the corresponding `<th>`/`<td>`;
2. Attributes at the end of a content row belong to the `<tr>` corresponding to that row; (Note: "End of row" refers to the position after the last vertical bar `|` in each line; there is no vertical bar `|` after attributes placed here)
3. Attributes within separator row cells belong to every `<th>`/`<td>` in the corresponding column;
4. Attributes at the end of a separator row belong to `<table>`.
```
| Corresponds to <th>                          | Corresponds to <tr>
| ===== Corresponds to all <th>/<td> in column | Corresponds to <table>
| Corresponds to <td>                          | Corresponds to <tr>
| ===== Corresponds to all <th>/<td> in column | Corresponds to <table>
| Corresponds to <td>                          | Corresponds to <tr>
```

**Parent Tag Attributes**:
1. Parent tag attributes within content row cells belong to the `<tr>` corresponding to that row (equivalent to standard attributes at the end of that row);
2. Parent tag attributes at the end of a content row belong to the `<thead>`/`<tbody>`/`<tfoot>` corresponding to that section;
3. Parent tag attributes within separator row cells are equivalent to standard attributes;
4. The parent tag notation for the title attribute at the end of a separator row (`[T< Table Title >T]`) will be parsed as `<caption>Table Title</caption>`, while parent tag notations for other attributes belong to `<table>` (equivalent to standard attributes).
```
| Corresponds to <tr>               | Corresponds to <thead>
| ===== same as standard attributes | Corresponds to <table> (Title attribute generates `<caption>` tag)
| Corresponds to <tr>               | Corresponds to <tbody>
| ===== same as standard attributes | Corresponds to <table>
| Corresponds to <tr>               | Corresponds to <tfoot>
```

---

### 4.4 Same-Attribute Conflicts

A same-attribute conflict occurs when multiple identical attributes are assigned to the same tag. This includes cases where multiple identical standard attributes are written repeatedly within the scope of a single tag, as well as cases where parent tag attributes from different positions pointing to the same parent tag. Below are two typical examples: Example 1 corresponds to the former case, and Example 2 corresponds to the latter.

Example 1: `This is a normal paragraph. [A[ center ]A]An align attribute appears here, and an align attribute appears at the end.[A[ right ]A]`.

Example 2:
```
1. Item one contains syntax that centers the parent tag [A< center >A];
2. Item two contains syntax that right-aligns the parent tag [A< right >A].
```

According to HTML attribute specifications, any given attribute can appear only once within a single tag. Therefore, when a same-attribute conflict occurs, only the last occurrence takes effect, and all previous ones are overridden. Accordingly, in both the examples above, only the align attribute right-aligns the target tag is retained, i.e. only ` align="right"` is parsed and output in the corresponding tag.

However, among HTML global attributes, the class attribute is unique in that it supports multiple coexisting values. Consequently, class attribute conflicts are handled differently from the override principle applied to other attributes; instead, an append principle is used. If the attribute abbreviation letter in the two examples above is changed from A to C, the parsed output will be `class="center right"`.

## 5. Escaping Rules

DrewMark syntax utilizes every symbol that can be typed directly from a keyboard. When the content a user wishes to write happens to match a DrewMark syntax exactly, the preferred solution is to wrap the relevant content using code syntax, which will output the original text conforming to DrewMark syntax verbatim. If using code syntax is inappropriate, or if the code syntax itself is the content that should not be parsed, then escaping rules must be employed. The escaping rule is quite simple: just add a backslash `\` before any DrewMark syntax marker. For example: `\**bold\**`, `*\*bold\**`, `*\*bold\**`, or `*\*bold*\*` will none of them be parsed as `<strong>bold</strong>`; instead, they will be output as raw text: `**bold**`. As another example, if you must wrap text in backticks but do not want it rendered as a `<code>` tag, simply write: `` \`not code\` ``.

There are several important notes regarding the use of escaping rules:

1. As shown in the two examples above, for enclosing-type syntax, you should escape at least one marker symbol in both the opening or closing marker parts. If you escape only one part while the same syntax is also used elsewhere in the surrounding context, the unescaped part may incorrectly match with its equivalent of the other same syntax, resulting in unintended parsing. This note applies not only to inline tags but also to block-level tags such as code blocks, figure blocks, details blocks, and style blocks, which are also enclosing-type syntaxes. The only difference is that these block-level tags use entire lines as their opening and closing markers; therefore, both the opening marker line and the closing marker line must be escaped simultaneously.
2. Link syntax combines two enclosed structures, yet it is easier to escape than typical enclosing-type syntax. You only need to escape either the left parenthesis (`\(){URL}`) or the left curly brace (`()\{URL}`), and it will not erroneously associate with other link syntax in the surrounding context. Inline image, audio, and video syntaxes are all based on link syntax, differing mainly in their prepended symbols. If you escape only the prepended symbol of these three syntaxes, i.e.  `\~(){URL}`, `\!(){URL}`, or `\$(){URL}`, the subsequent `(){}` portion still conforms to link syntax and will therefore be parsed as the respective prepended symbol followed by an `<a>` tag. The correct way to escape these three syntaxes is the same as for link syntax: escape either the left parenthesis or the left curly brace.
3. To escape syntaxes that rely on line-start markers, such as quote blocka and lists, simply add a backslash before the line-start marker. This method also works for tables; however, escaping a content row of a table does not prevent other rows from still conforming to table syntax. To escape an entire table, you must add a backslash before every row of the tabel.
4. Inline image syntax cannot be escaped within a figure block, because figure blocks support only two types of lines: lines beginning with an exclamation mark followed by a space correspond to the `<figcaption>` tag; lines containing inline image syntax have only the inline image portion parsed, while all other content is discarded. Once an inline image within a figure block is escaped, that escaped inline image syntax also falls into the discarded range.

The backslash `\`, when used as an escape character, is always hidden unless it appears at the end of a line. If a backslash must be visible within a line, you must also escape it: every two consecutive backslashes are rendered as a single backslash, i.e. `\\` is parsed as `\`.

### 5.1 Special Case Where Escaping Is Ineffective

As mentioned earlier, any DrewMark syntax markers written inside inline code or code blocks are output as-is. However, there is yet one exception: the backtick (`` ` ``), since it is the very marker used to define these two syntax themselves. If you need to display a backtick within inline code, or three or more consecutive backticks at the beginning of a line within a code block, using a backslash for escaping will not wor, because backslash itself will be rendered as-is in these two syntax contexts and cannot function as an escape character. To handle this special case, you must rely on the quantity of backticks: the number of enclosing backticks must be greater than the number of backticks you wish to display.

---

*Version: v2.3*