# Nordic EPUB 2025-1 Detailed Checklist

Complete checklist for **Nordic Guidelines for Production of Accessible EPUB 3, version 2025-1**. Use this checklist only when the EPUB declares 2025-1 (e.g. `nordic:guidelines` or `dcterms:conformsTo`).

For EPUBs declaring **2015-1** or **2020-1**, use the version-specific checklists instead:

- [nordic-epub-checklist-2015-1.md](nordic-epub-checklist-2015-1.md)
- [nordic-epub-checklist-2020-1.md](nordic-epub-checklist-2020-1.md)

## Package Document (package.opf)

### Root Element

```xml
<package xmlns="http://www.idpf.org/2007/opf"
         xmlns:dc="http://purl.org/dc/elements/1.1/"
         prefix="nordic: http://www.mtm.se/epub/"
         version="3.0"
         xml:lang="[publication language]"
         unique-identifier="pub-identifier">
```

- [ ] `xmlns` namespace correct
- [ ] `xmlns:dc` namespace correct
- [ ] `prefix` includes `nordic:`
- [ ] `version="3.0"`
- [ ] `xml:lang` matches publication language
- [ ] `unique-identifier` references `dc:identifier`

### Required Metadata

- [ ] `dc:title id="title"` present
- [ ] `dc:language` with valid code (nb, nn, sv, da, fi, etc.)
- [ ] `dc:identifier id="pub-identifier"` matches filename UID
- [ ] `dc:source` contains ISBN
- [ ] `dc:creator` for each author
- [ ] `dc:publisher` (ordering agency shorthand)
- [ ] `dc:date` in ISO format
- [ ] `meta property="dcterms:modified"` present
- [ ] `meta property="nordic:supplier"` present
- [ ] `meta property="nordic:guidelines"` equals `2025-1`

### Accessibility Metadata

Minimum required:

- [ ] `schema:accessMode` - at least `textual`
- [ ] `schema:accessModeSufficient` - at least `textual`
- [ ] `schema:accessibilityFeature` includes:
  - [ ] `displayTransformability`
  - [ ] `structuralNavigation`
  - [ ] `tableOfContents`
  - [ ] `readingOrder`
- [ ] `schema:accessibilityHazard` - `none` or specific hazards
- [ ] `dcterms:conformsTo` links to guidelines URL
- [ ] `a11y:certifiedBy` present

If images with descriptions:

- [ ] `schema:accessMode` includes `visual`
- [ ] `schema:accessibilityFeature` includes `alternativeText`
- [ ] `schema:accessibilityFeature` includes `longDescription` (if applicable)

If pagination:

- [ ] `schema:accessibilityFeature` includes `pageBreakMarkers`
- [ ] `schema:accessibilityFeature` includes `pageNavigation`
- [ ] `pageBreakSource` with ISBN

If MathML:

- [ ] `schema:accessibilityFeature` includes `MathML`

### Manifest

- [ ] All content files listed with correct `media-type`
- [ ] Navigation document has `properties="nav"`
- [ ] Cover image has `properties="cover-image"`
- [ ] MathML content files have `properties="mathml"`
- [ ] All `href` paths are relative and correct

### Spine

- [ ] All content documents in `itemref` elements
- [ ] Reading order is correct
- [ ] Cover `itemref` has `linear="no"`
- [ ] `idref` values match manifest `id` values

## Navigation Document (nav.xhtml)

### Document Structure

- [ ] XML declaration: `<?xml version="1.0" encoding="utf-8"?>`
- [ ] DOCTYPE: `<!DOCTYPE html>`
- [ ] Correct namespaces on `<html>`
- [ ] `<title>` matches main heading
- [ ] Links to CSS stylesheet

### Table of Contents

```html
<nav role="doc-toc" aria-labelledby="n1" epub:type="toc">
  <h1 id="n1">[Language-specific heading]</h1>
  <ol>...</ol>
</nav>
```

- [ ] `role="doc-toc"` present
- [ ] `epub:type="toc"` present
- [ ] `aria-labelledby` references heading `id`
- [ ] Heading is `<h1>`
- [ ] All body headings included (except `class="no-toc"`)
- [ ] Heading levels implied through nesting
- [ ] Links point to section elements, not headings
- [ ] Title page referenced as "Tittelside" (Norwegian)

### Page List (if paginated)

```html
<nav role="doc-pagelist" aria-labelledby="n2" epub:type="page-list">
  <h1 id="n2">[Language-specific heading]</h1>
  <ol>...</ol>
</nav>
```

- [ ] `role="doc-pagelist"` present
- [ ] `epub:type="page-list"` present
- [ ] All page breaks listed
- [ ] Labels match `aria-label` values

### Landmarks (if present)

- [ ] `epub:type="landmarks"` present
- [ ] Links to major sections (TOC, bodymatter start, etc.)

## Content Documents

### XHTML Requirements

- [ ] XML declaration present
- [ ] DOCTYPE present
- [ ] `<html>` has all required namespaces
- [ ] `xml:lang` and `lang` set correctly
- [ ] `<meta name="dc:identifier">` matches package
- [ ] `<meta name="viewport" content="width=device-width"/>`
- [ ] `<title>` matches document's main heading

### Proper XHTML Markup

Content documents must be well-formed XHTML5 and use valid structure so that reading systems and assistive technologies can parse and expose content correctly.

- [ ] **Well-formed XML**: All elements properly closed (including self-closing form e.g. `<br/>`, `<img ... />`); all attribute values in double quotes; no unescaped `<` or `&` in text (use entities or CDATA where needed).
- [ ] **Document structure**: Root `<html>`; exactly one `<head>` and one `<body>`; no text or elements outside the document tree.
- [ ] **Valid nesting**: Block elements (e.g. `<p>`, `<div>`, `<section>`) not inside inline elements (e.g. `<a>`, `<span>`); heading hierarchy and list structure (e.g. `<ul>`/`<ol>` only with `<li>` children) correct.
- [ ] **Character encoding**: File saved as UTF-8; XML declaration encoding matches; special characters either UTF-8 or valid entities (e.g. `&amp;`, `&lt;`, `&nbsp;` where required).
- [ ] **No deprecated markup**: No `<font>`, `<center>`, `<strike>`, presentational attributes (e.g. `align`, `bgcolor`); use CSS and semantic elements instead.
- [ ] **IDs unique**: Every `id` attribute is unique within the document; no duplicate `id` values.

EPUBCheck or similar validators can catch many well-formedness and structure errors; manual review should confirm semantic and Nordic-specific requirements.

### File Naming

Pattern: `[UID]-[XXX]-[role].xhtml`

- [ ] UID matches `dc:identifier`
- [ ] XXX is zero-padded sequence number
- [ ] role matches section's ARIA role (minus "doc-")

### Structural Semantics

Top-level sections require:

- [ ] `role` attribute (from DPUB-ARIA)
- [ ] `epub:type` with partition value (`frontmatter`, `bodymatter`, `backmatter`)
- [ ] `aria-labelledby` if section has heading
- [ ] `aria-label` if section has no heading

### Headings

A logical heading hierarchy (no skipped levels) lets screen readers and other assistive technologies navigate by headings and understand document structure.

- [ ] Correct hierarchy (no skipped levels)
- [ ] Top-level content headings are `<h1>` (or `<h2>` in parts)
- [ ] `<hgroup>` for heading + subtitle combinations
- [ ] Subtitles use `<p epub:type="subtitle" role="doc-subtitle">`
- [ ] Chapter numbers in `<span class="chnum">` or `<span class="partnum">`

### Pagination

Block page break:

```html
<div epub:type="pagebreak" role="doc-pagebreak" 
     class="page-normal" id="page-38" aria-label="38"/>
```

Inline page break:

```html
<span epub:type="pagebreak" role="doc-pagebreak" 
      class="page-normal" id="page-38" aria-label="38"/>
```

- [ ] `epub:type="pagebreak"` present
- [ ] `role="doc-pagebreak"` present
- [ ] `class` is `page-front`, `page-normal`, or `page-special`
- [ ] `id` is unique
- [ ] `aria-label` matches page number
- [ ] No unnumbered pages

### Images

Figure with image:

```html
<figure class="image">
  <figcaption>...</figcaption>
  <img src="images/X41001A-012.jpg" alt="[type]" aria-describedby="desc012"/>
  <aside class="fig-desc" id="desc012">
    <p>...</p>
  </aside>
</figure>
```

- [ ] `<figure class="image">` wrapper
- [ ] `<img>` has `alt` attribute (never empty)
- [ ] Alt text uses standard values or meaningful description
- [ ] `<figcaption>` for captions
- [ ] `aria-describedby` links to description if present
- [ ] Image series wrapped in `<figure class="image-series">`

Image file requirements:

- [ ] Stored in `EPUB/images/`
- [ ] Named `[UID]-[XXX].[jpg|png]`
- [ ] Cover named `cover.jpg` or `cover.png`
- [ ] Max 800px on longest side (unless text legibility requires more)

### Tables

```html
<table>
  <caption>...</caption>
  <thead>
    <tr><th>...</th></tr>
  </thead>
  <tbody>
    <tr><td>...</td></tr>
  </tbody>
</table>
```

- [ ] `<caption>` for table title
- [ ] `<thead>` for header rows
- [ ] `<th>` for header cells
- [ ] `scope` attribute when headers span or are not in first row/column
- [ ] Consistent cell count per row
- [ ] No layout-only tables

### Notes

End notes:

```html
<section role="doc-endnotes" epub:type="endnotes">
  <h2>Notes</h2>
  <ol>
    <li id="fn1">
      <p>Note text</p>
      <p><a href="#ref1" role="doc-backlink">Go to note reference 1.</a></p>
    </li>
  </ol>
</section>
```

Note references:

```html
<a id="ref1" href="#fn1" role="doc-noteref" epub:type="noteref">1</a>
```

- [ ] References have `role="doc-noteref"` and `epub:type="noteref"`
- [ ] Notes have unique `id`
- [ ] Backlinks have `role="doc-backlink"`
- [ ] One-to-one relationship between references and notes

### Lists

- [ ] `<ol>` for numbered lists (no manual numbering)
- [ ] `<ul>` for unnumbered lists
- [ ] `<ul class="plain">` for lists without markers
- [ ] `<dl>` for definition/description lists
- [ ] TOC in source uses `<ol class="plain" epub:type="toc" role="doc-toc">`

### Poetry/Verse

```html
<div class="verse">
  <p class="linegroup">
    <span class="line">First line</span><br/>
    <span class="line">Second line</span>
  </p>
</div>
```

- [ ] `<div class="verse">` wrapper
- [ ] `<p class="linegroup">` for stanzas
- [ ] `<span class="line">` for individual lines
- [ ] `<br/>` between lines in same group

### Language Tagging

- [ ] Block-level language changes have `lang` and `xml:lang`
- [ ] Language codes from IANA registry
- [ ] Most specific code used (nb/nn not just no)

## Special Content

### Cover

- [ ] Separate XHTML file
- [ ] `<section epub:type="cover">`
- [ ] `<img role="doc-cover">`
- [ ] `linear="no"` in spine

### Title Page

- [ ] `<h1 epub:type="title" class="title">`
- [ ] `<p epub:type="subtitle" role="doc-subtitle">` for subtitle
- [ ] `<p class="docauthor">` for authors

### Computer Code

- [ ] `<code>` for inline code
- [ ] `<pre><code>` for code blocks
- [ ] Whitespace preserved

### Text Emphasis

- [ ] `<strong>` for bold
- [ ] `<em>` for italics
- [ ] `<span class="underline">` for underline

### Thematic Breaks

- [ ] `<hr class="emptyline"/>` for vertical space breaks
- [ ] `<hr class="separator"/>` for visual markers
