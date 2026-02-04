# Nordic EPUB 2015-1 Checklist

Checklist for **Nordic Guidelines for Production of Accessible EPUB 3, version 2015-1**. Use only when the EPUB declares 2015-1 (`nordic:guidelines` or `dcterms:conformsTo`).

**Verify requirements against the official guideline:** [Nordic EPUB 2015-1](https://format.mtm.se/nordic_epub/2015-1/). This checklist reflects typical 2015-1 requirements; the official document is authoritative. For full structural detail (images, tables, notes, lists, etc.) see [nordic-epub-checklist.md](nordic-epub-checklist.md) and apply only the 2015-1 relaxations listed below.

## Version-specific rules (2015-1)

Compared with 2025-1, 2015-1 does **not** require:

- `role="doc-toc"` / `role="doc-pagelist"` on nav elements (epub:type is sufficient)
- `role="doc-pagebreak"` on page break elements (epub:type="pagebreak" is sufficient)
- The full 2025-1 accessibility metadata set; consult the 2015-1 spec for the required set

## Package Document (package.opf)

### Root element and required metadata

- [ ] Package namespaces, version 3.0, xml:lang, unique-identifier
- [ ] `dc:title`, `dc:language`, `dc:identifier id="pub-identifier"`, `dc:source`, `dc:creator`, `dc:publisher`, `dc:date`
- [ ] `meta property="dcterms:modified"`
- [ ] `meta property="nordic:supplier"`
- [ ] `meta property="nordic:guidelines"` equals **2015-1**

### Accessibility metadata

- [ ] Consult the official 2015-1 guideline for the required accessibility metadata set. Do not require the full 2025-1 set unless the spec aligns.

### Manifest and spine

- [ ] All content files, correct media-type; nav has `properties="nav"`; cover image; MathML when present
- [ ] Spine: correct reading order, cover `linear="no"`

## Navigation Document (nav.xhtml)

### Table of contents

- [ ] **`epub:type="toc"`** present (required)
- [ ] `role="doc-toc"` **not** required for 2015-1 (optional)
- [ ] Heading and list structure; links to sections

### Page list (if paginated)

- [ ] **`epub:type="page-list"`** when paginated (required)
- [ ] `role="doc-pagelist"` **not** required for 2015-1 (optional)
- [ ] Page list matches page breaks in content

### Landmarks

- [ ] Optional; `epub:type="landmarks"` if present

## Content documents

### Structure and headings

- [ ] XML/DOCTYPE; html namespaces; xml:lang and lang
- [ ] Section semantics (epub:type / role as per 2015-1 spec)
- [ ] Heading hierarchy (no skipped levels)

### Page breaks

- [ ] **`epub:type="pagebreak"`** present on page break elements (required)
- [ ] `role="doc-pagebreak"` **not** required for 2015-1 (optional)
- [ ] id and page number alignment with page-list

### Images and tables

- [ ] `<img>` has `alt`; figures with figcaption where appropriate
- [ ] Tables: caption, thead, th with scope where appropriate

### Other

- [ ] Cover, title page, lists, language tagging: follow 2015-1 guideline where specified

## Reference

- Nordic EPUB Guidelines 2015-1: <https://format.mtm.se/nordic_epub/2015-1/>
