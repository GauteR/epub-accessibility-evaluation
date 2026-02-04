# EPUB Accessibility Evaluation

A Cursor/skills.sh skill that evaluates **unzipped** EPUB files against the Nordic Accessible EPUB Guidelines (2015-1, 2020-1, or 2025-1), WCAG 2.2, and Nordic MathML Guidelines. Validation uses only the guideline version the EPUB declares in its package metadata.

## Installation

With the [skills](https://skills.sh/docs/cli) CLI:

```bash
npx skills add <owner>/epub-accessibility-evaluation
```

For Cursor, add the skill to your project or user skills directory (e.g. `.cursor/skills/epub-accessibility-evaluation/`) and ensure `SKILL.md` plus the reference checklists are present.

## Requirements

- The EPUB must be **unzipped**. Provide the path to the unpacked EPUB directory (containing `META-INF/`, `EPUB/`, `mimetype`, etc.).

## What It Validates

- **Phase 0**: Reads `package.opf` to determine declared guideline (2015-1, 2020-1, or 2025-1). If none is declared, evaluation defaults to 2025-1.
- **Phase 1–2**: Package metadata, accessibility metadata, navigation (TOC, page-list), content structure, images, tables, MathML (if present), and page breaks — all according to the **declared** version only.
- **Phase 3**: Produces a structured report (summary table, critical/warning/recommendation lists, references).

Version-specific rules (e.g. nav roles, page-break roles, required accessibility metadata) are applied only for the declared version; requirements from other versions are not reported as failures.

## References

- Nordic EPUB Guidelines: [format.mtm.se/nordic_epub](https://format.mtm.se/nordic_epub/) (2015-1, 2020-1, 2025-1)
- Nordic MathML Guidelines: [github.com/nlbdev/mathml-guidelines](https://github.com/nlbdev/mathml-guidelines)
- WCAG 2.2: [w3.org/TR/WCAG22](https://www.w3.org/TR/WCAG22/)

## Repository Structure

| File | Purpose |
|------|---------|
| `SKILL.md` | Main skill instructions and report template |
| `nordic-epub-checklist.md` | 2025-1 detailed checklist |
| `nordic-epub-checklist-2015-1.md` | 2015-1 checklist |
| `nordic-epub-checklist-2020-1.md` | 2020-1 checklist |
| `mathml-checklist.md` | MathML validation checklist |
| `wcag-mapping.md` | Mapping of Nordic requirements to WCAG 2.2 |
