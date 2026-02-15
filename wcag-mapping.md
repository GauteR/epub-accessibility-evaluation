# WCAG 2.2 Mapping for Nordic EPUB Guidelines

How Nordic EPUB requirements map to WCAG 2.2 success criteria.

## Perceivable (Principle 1)

### 1.1 Text Alternatives

| WCAG SC | Level | Nordic Requirement |
| --- | ---------------- | ------------------ |
| 1.1.1 Non-text Content | A | Images have `alt` attribute; decorative images handled appropriately |

**Nordic implementation:**

- All `<img>` elements require `alt` attribute
- Use standard alt text values (Photo., Illustration., etc.)
- Extended descriptions via `aria-describedby` and `<aside class="fig-desc">`
- Cover image has `role="doc-cover"`

**Note:** Nordic guidelines allow generic alt text; full WCAG compliance may require meaningful descriptions.

### 1.3 Adaptable

| WCAG SC | Level | Nordic Requirement |
| --- | ---------------- | ------------------ |
| 1.3.1 Info and Relationships | A | Semantic HTML structure, proper heading hierarchy, table markup |
| 1.3.2 Meaningful Sequence | A | Correct reading order in spine, linear navigation |

**Nordic implementation:**

- `<section>` with `role` and `epub:type` for semantic structure
- Heading levels follow document hierarchy
- Tables use `<caption>`, `<thead>`, `<th scope>`
- Lists use appropriate `<ol>`, `<ul>`, `<dl>` elements
- Reading order defined by spine sequence

### 1.4 Distinguishable

| WCAG SC | Level | Nordic Requirement |
| --- | ---------------- | ------------------ |
| 1.4.4 Resize Text | AA | CSS-based styling allows text resizing |

**Nordic implementation:**

- Standard CSS provided by ordering agency
- No fixed font sizes
- Content adapts to user settings

## Operable (Principle 2)

### 2.4 Navigable

| WCAG SC | Level | Nordic Requirement |
| --- | ---------------- | ------------------ |
| 2.4.1 Bypass Blocks | A | Navigation document with TOC |
| 2.4.2 Page Titled | A | Content documents have descriptive `<title>` |
| 2.4.5 Multiple Ways | AA | TOC, page list, landmarks |
| 2.4.6 Headings and Labels | AA | Descriptive headings, proper heading structure |

**Nordic implementation:**

- `nav.xhtml` with `role="doc-toc"`
- Page list for paginated content
- Landmarks navigation (optional)
- `<title>` matches main heading of each document
- Headings describe content, follow hierarchy

## Understandable (Principle 3)

### 3.1 Readable

| WCAG SC | Level | Nordic Requirement |
| --- | ---------------- | ------------------ |
| 3.1.1 Language of Page | A | `xml:lang` and `lang` on root element |
| 3.1.2 Language of Parts | AA | Language attributes on content in other languages |

**Nordic implementation:**

- `<html xml:lang="nb" lang="nb">` (example for Norwegian Bokmål)
- Block-level language changes tagged with both attributes
- Use specific language codes (nb, nn, sv, da, fi, etc.)

**Note:** Nordic guidelines only require block-level language tagging; inline tagging optional.

## Robust (Principle 4)

### 4.1 Compatible

| WCAG SC | Level | Nordic Requirement |
| --- | ---------------- | ------------------ |
| 4.1.2 Name, Role, Value | A | ARIA roles, proper semantic markup |

**Nordic implementation:**

- Sections have `role` (DPUB-ARIA) and `epub:type`
- Notes use `role="doc-noteref"`, `role="doc-backlink"`, etc.
- Interactive elements properly labeled
- Page breaks have `role="doc-pagebreak"`

## EPUB Accessibility Specification Mapping

The Nordic Guidelines implement [EPUB Accessibility 1.1](https://www.w3.org/TR/epub-a11y-11/):

### Discovery Metadata (Section 2)

- [ ] `schema:accessMode` identifies content modes
- [ ] `schema:accessModeSufficient` specifies sufficient modes
- [ ] `schema:accessibilityFeature` lists features
- [ ] `schema:accessibilityHazard` declares hazards
- [ ] `schema:accessibilitySummary` (when required)

### Conformance (Section 3)

- [ ] `dcterms:conformsTo` references guidelines URL
- [ ] `a11y:certifiedBy` identifies certifying organization

## Areas Where Nordic May Not Meet Full WCAG

### 1.1.1 Non-text Content (Partial)

Nordic allows generic alt text values. For full WCAG compliance:

- Images need meaningful descriptions
- Complex images need long descriptions

### 3.1.2 Language of Parts (Partial)

Nordic requires block-level language tagging only. For full WCAG compliance:

- Inline language changes should also be tagged

### Color and Contrast

Nordic guidelines defer to CSS styling; no specific contrast requirements beyond WCAG.

## Validation Against WCAG

### Tools

- [EPUBCheck](https://www.w3.org/publishing/epubcheck/) - Structural validity
- [Ace by DAISY](https://daisy.github.io/ace/) - Accessibility evaluation
- [Nordic EPUB Validator](https://nlbdev.github.io/nordic-epub3-dtbook-migrator/) - Nordic guidelines compliance

### Checklist for WCAG Level A

Essential items for Level A:

- [ ] All images have alt text
- [ ] Document language specified
- [ ] Headings in logical order
- [ ] Lists marked up as lists
- [ ] Tables have headers
- [ ] Navigation document present
- [ ] Page titles descriptive

### Checklist for WCAG Level AA

Additional items for Level AA:

- [ ] Language of parts marked
- [ ] Multiple ways to find content
- [ ] Consistent navigation structure
- [ ] Error identification (if forms present)

## DAISY Knowledge Base References

Key resources from [DAISY KB](https://kb.daisy.org/publishing/docs/):

- [HTML Semantics](https://kb.daisy.org/publishing/docs/html/)
- [Images](https://kb.daisy.org/publishing/docs/html/images.html)
- [Tables](https://kb.daisy.org/publishing/docs/html/tables.html)
- [Navigation](https://kb.daisy.org/publishing/docs/navigation/)
- [Metadata](https://kb.daisy.org/publishing/docs/metadata/)
- [MathML](https://kb.daisy.org/publishing/docs/html/mathml.html)
