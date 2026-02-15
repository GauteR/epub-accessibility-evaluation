# Nordic EPUB Evaluation

A [Skill](https://skills.sh) that evaluates **unzipped** EPUB files against the Nordic Accessible EPUB Guidelines (2015-1, 2020-1, or 2025-1), WCAG 2.2, and MathML (Nordic checklist and NLB production). Validation uses only the guideline version the EPUB declares in its package metadata; MathML is checked against both checklists and the report includes a short summary of differences between them.

## Prerequisites: Node.js and npx

The installation command uses `npx`, which comes with **Node.js**. If you don't have Node.js yet:

1. **Download Node.js** from [nodejs.org](https://nodejs.org/). Choose the LTS version.
2. **Run the installer** and follow the steps (default options are fine).
3. **Restart** any open terminal or command prompt.
4. **Check that it works**: open a terminal and run:
   - `node --version` — you should see a version number (e.g. 20.x.x).
   - `npx --version` — you should also see a version number.

If you see "command not found" or similar, Node.js is not installed or not on your PATH; run the installer again or add Node.js to your system PATH.

## Installation

Open a terminal in the folder where you want to use the skill and run:

```bash
npx skills add https://github.com/gauter/nordic-epub-evaluation --skill nordic-epub-evaluation
```

When you run `npx skills add …`, you can choose which agent to install the skill for. The skills installer supports **Cursor**, **GitHub Copilot**, **Claude**, and others. Select the agent you use so the skill is installed in the right place.

## Requirements

Either:

- Show the agent where it can find the EPUB. The EPUB must be **unzipped**. Provide the path to the unpacked EPUB directory (containing `META-INF/`, `EPUB/`, `mimetype`, etc.).
- Or open a project with the EPUB in it's unzipped for in it. (Or in the future, use MCP to get the unzipped file from the filesystem)

## What It Validates

- **Phase 0**: Reads `package.opf` to determine declared guideline (2015-1, 2020-1, or 2025-1). If none is declared, evaluation defaults to 2025-1.
- **Phase 1–2**: Package metadata, accessibility metadata, navigation (TOC, page-list), content structure, images, tables, MathML (if present) against **both** Nordic and NLB production checklists, and page breaks — all according to the **declared** version only.
- **Phase 3**: Produces a structured report (summary table with separate rows for MathML (Nordic) and MathML (NLB production), critical/warning/recommendation lists, short summary of MathML guideline differences, references).

Version-specific rules (e.g. nav roles, page-break roles, required accessibility metadata) are applied only for the declared version; requirements from other versions are not reported as failures.

## References

- Nordic EPUB Guidelines: [format.mtm.se/nordic_epub](https://format.mtm.se/nordic_epub/) (2015-1, 2020-1, 2025-1)
- Nordic MathML Guidelines: [github.com/nlbdev/mathml-guidelines](https://github.com/nlbdev/mathml-guidelines)
- WCAG 2.2: [w3.org/TR/WCAG22](https://www.w3.org/TR/WCAG22/)

## Repository Structure

| File | Purpose |
| ------ | --------- |
| `SKILL.md` | Main skill instructions and report template |
| `nordic-epub-checklist.md` | 2025-1 detailed checklist |
| `nordic-epub-checklist-2015-1.md` | 2015-1 checklist |
| `nordic-epub-checklist-2020-1.md` | 2020-1 checklist |
| `mathml-checklist.md` | MathML validation (Nordic checklist) |
| `mathml-checklist-nlb-production.md` | MathML validation (NLB production / old checklist) |
| `mathml-guidelines-differences.md` | Comparison of NLB production vs. Nordic checklist; used in the report |
| `wcag-mapping.md` | Mapping of Nordic requirements to WCAG 2.2 |
