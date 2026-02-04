# Nordic EPUB 2020-1 Checklist

Checklist for **Nordic Guidelines for Production of Accessible EPUB 3, version 2020-1**. Use only when the EPUB declares 2020-1 (`nordic:guidelines` or `dcterms:conformsTo`).

**Verify requirements against the official guideline:** [Nordic EPUB 2020-1](https://format.mtm.se/nordic_epub/2020-1/). This checklist reflects typical 2020-1 requirements; the official document is authoritative. For full structural detail (images, tables, notes, lists, etc.) see [nordic-epub-checklist.md](nordic-epub-checklist.md) and apply only the 2020-1 relaxations listed below.

## Version-specific rules (2020-1)

- **Nav:** `epub:type="toc"` and `epub:type="page-list"` required; **`role="doc-toc"` and `role="doc-pagelist"` recommended** (not required as in 2025-1).
- **Page breaks:** `epub:type="pagebreak"` required; **`role="doc-pagebreak"` recommended** (not required as in 2025-1).
- **Accessibility metadata:** Consult the 2020-1 spec for the required set; the 2025-1 set may be stricter.

## Package Document (package.opf)

### Root element and required metadata

- [ ] Package namespaces, version 3.0, xml:lang, unique-identifier
- [ ] `dc:title`, `dc:language`, `dc:identifier id="pub-identifier"`, `dc:source`, `dc:creator`, `dc:publisher`, `dc:date`
- [ ] `meta property="dcterms:modified"`
- [ ] `meta property="nordic:supplier"`
- [ ] `meta property="nordic:guidelines"` equals **2020-1**

### Accessibility metadata

- [ ] Consult the official 2020-1 guideline for the required accessibility metadata set.

### Manifest and spine

- [ ] All content files, correct media-type; nav has `properties="nav"`; cover image; MathML when present
- [ ] Spine: correct reading order, cover `linear="no"`

## Navigation Document (nav.xhtml)

### Table of contents

- [ ] **`epub:type="toc"`** present (required)
- [ ] **`role="doc-toc"`** recommended for 2020-1 (not required)
- [ ] Heading and list structure; links to sections

### Page list (if paginated)

- [ ] **`epub:type="page-list"`** when paginated (required)
- [ ] **`role="doc-pagelist"`** recommended for 2020-1 (not required)
- [ ] Page list matches page breaks in content

### Landmarks

- [ ] Optional; `epub:type="landmarks"` if present

## Content documents

### Structure and headings

- [ ] XML/DOCTYPE; html namespaces; xml:lang and lang
- [ ] Section semantics (epub:type / role as per 2020-1 spec)
- [ ] Heading hierarchy (no skipped levels)

### Page breaks

- [ ] **`epub:type="pagebreak"`** present (required)
- [ ] **`role="doc-pagebreak"`** recommended for 2020-1 (not required)
- [ ] id and page number alignment with page-list

### Images and tables

- [ ] `<img>` has `alt`; figures with figcaption where appropriate
- [ ] Tables: caption, thead, th with scope where appropriate

### Other

- [ ] Cover, title page, lists, language tagging: follow 2020-1 guideline where specified

## Reference

- Nordic EPUB Guidelines 2020-1: https://format.mtm.se/nordic_epub/2020-1/
