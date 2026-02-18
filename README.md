# Nordic EPUB Evaluation

A [Skill](https://skills.sh) that evaluates **unzipped** EPUB files against the Nordic Accessible EPUB Guidelines (2015-1, 2020-1, or 2025-1), WCAG 2.2, and MathML. Validation uses only the guideline version the EPUB declares in its package metadata. When MathML is present, one MathML checklist is used depending on the declared version: **2015-1** → NLB MathML guidelines; **2020-1 or 2025-1** → Nordic MathML guidelines.

## Prerequisites: Node.js and npx

The installation command uses `npx`, which comes with **Node.js**. If you don't have Node.js yet:

1. **Download Node.js** from [nodejs.org](https://nodejs.org/). Choose the LTS version.
2. **Run the installer** and follow the steps (default options are fine).
3. **Restart** any open terminal or command prompt.
4. **Check that it works**: open a terminal and run:
   - `node --version` — you should see a version number.
   - `npx --version` — you should also see a version number.

If you see "command not found" or similar, Node.js is not installed or not on your PATH; run the installer again or add Node.js to your system PATH.

## Installation

Open a terminal in the folder where you want to use the skill and run:

```bash
npx skills add https://github.com/gauter/nordic-epub-evaluation --skill nordic-epub-evaluation
```

When you run `npx skills add …`, you can choose which agent to install the skill for. The skills installer supports **Cursor**, **GitHub Copilot**, **Claude**, and others. Select the agent you use so the skill is installed in the right place.

## How to contribute

1. **Clone** the repository and create a branch for your changes (e.g. from `main`).
2. **Edit the right files.** The workflow and report template live in `SKILL.md`. Version-specific requirements live in the checklist files (`nordic-epub-checklist.md`, `nordic-epub-checklist-2015-1.md`, `nordic-epub-checklist-2020-1.md`, and the MathML checklists). Keep `SKILL.md` and the checklists aligned: if you add or change a requirement in a checklist, update the quick reference and any phase descriptions in `SKILL.md` that refer to it.
3. **Respect version boundaries.** The skill validates only the guideline version the EPUB declares. When changing requirements, ensure they are scoped to the correct version (2015-1, 2020-1, or 2025-1) and that the version-specific table in `SKILL.md` stays accurate.
4. **Open a pull request** with a short description of what changed and why. If the change affects the report format or severity rules, mention it so reviewers can check the report template and examples.

## How to work with this skill

1. **Unzip the EPUB.** The skill only evaluates **unzipped** EPUB directories (with `META-INF/`, `EPUB/`, `mimetype`, etc.). Unzip the EPUB, e.g. `unzip book.epub -d book-unzipped`.
2. **Give the agent access to the folder.** Open the project that contains the unzipped EPUB directory, or provide the path when you ask for an evaluation.
3. **Request an evaluation.**

   ```text
   # For example
   Evaluate the EPUB at [path] against the Nordic guidelines

   # or
   Run nordic-epub-evaluation on [path]
   ```

   The agent will use the skill and run Phases 0–3 (identify declared guideline version → structure and content checks → report).

4. **The report.** You get a structured report with a summary table, detailed findings (file, line, requirement, action), and references. Use the table to fix issues systematically.

The skill validates only against the guideline version the EPUB declares in `package.opf`; requirements from other versions are not reported as failures.

## References

- Nordic EPUB Guidelines: [format.mtm.se/nordic_epub](https://format.mtm.se/nordic_epub/) (2015-1, 2020-1, 2025-1)
- Nordic MathML Guidelines: [github.com/nlbdev/mathml-guidelines](https://github.com/nlbdev/mathml-guidelines)
- WCAG 2.2: [w3.org/TR/WCAG22](https://www.w3.org/TR/WCAG22/)

## Repository structure

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
