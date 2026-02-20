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

## How to work with this skill

1. **Unzip the EPUB.** The skill only evaluates **unzipped** EPUB directories (with `META-INF/`, `EPUB/`, `mimetype`, etc.). Unzip the EPUB, e.g. `unzip book.epub -d book-unzipped`.
2. **Give the agent access to the folder.** Open the project that contains the unzipped EPUB directory, or provide the path when you ask for an evaluation.
3. **Request an evaluation.** Use one of the prompts in [Commands and example prompts](#commands-and-example-prompts) below (or similar). The agent will use the skill and run Phases 0–3 (identify declared guideline version → structure and content checks → report).
4. **The report.** You get a structured report with a summary table, detailed findings (file, line, requirement, action), and references. Use the table to fix issues systematically.

Validation uses only the guideline version the EPUB declares in `package.opf`; requirements from other versions are not reported as failures.

### Commands and example prompts

You can paste or adapt these when asking the agent to run the skill:

- **Full evaluation**
  - *"Evaluate the EPUB at [path] against the Nordic guidelines."*
  - *"Run nordic-epub-evaluation on [path]."*

- **Include the MathML upgrade addendum (diff: NLB → Nordic MathML)**  
  For EPUBs that declare **2015-1** and contain MathML, the skill instructs the agent to add an addendum based on `mathml-guidelines-differences.md` (what would need to change to comply with the Nordic MathML Guidelines). You can request it explicitly, for example:
  - *"Evaluate this EPUB and include the MathML upgrade addendum (differences between NLB and Nordic MathML guidelines)."*  
  For 2015-1 EPUBs with MathML, the addendum is included automatically in the report.

- **Report on upgrading to a newer EPUB guideline version**  
  To get a report on what would need to change to move from the declared version to a newer Nordic EPUB version (e.g. 2015-1 or 2020-1 → 2025-1), ask for example:
  - *"Evaluate this EPUB and report what would need to change to upgrade from the declared version to 2025-1."*  
  The agent uses the version-specific requirements in `SKILL.md` and the checklist files to describe the differences.

- **More targeted requests** (if the agent supports them)
  - *"Run only Phase 0 and report the declared guideline version."*
  - *"Run only navigation checks for this EPUB."*
  - *"Run only the MathML checklist for this EPUB."*

## How to contribute

If you use Git locally (clone, branch, commit from a terminal), follow the steps below. If you prefer to edit only in the browser without technical setup, see [How to update the skill (step-by-step)](#how-to-update-the-skill-step-by-step) instead.

1. **Clone** the repository and create a branch for your changes (e.g. from `main`).
2. **Edit the right files.** The workflow and report template live in `SKILL.md`. Version-specific requirements live in the checklist files (`nordic-epub-checklist.md`, `nordic-epub-checklist-2015-1.md`, `nordic-epub-checklist-2020-1.md`, and the MathML checklists). Keep `SKILL.md` and the checklists aligned: if you add or change a requirement in a checklist, update the quick reference and any phase descriptions in `SKILL.md` that refer to it.
3. **Respect version boundaries.** The skill validates only the guideline version the EPUB declares. When changing requirements, ensure they are scoped to the correct version (2015-1, 2020-1, or 2025-1) and that the version-specific table in `SKILL.md` stays accurate.
4. **Open a pull request** with a short description of what changed and why. If the change affects the report format or severity rules, mention it so reviewers can check the report template and examples.

## How to update the skill (step-by-step)

This section is for contributors who want to edit the skill in the browser without using Git or a terminal. You work directly on a **branch in the main repository** and open a pull request when done.

**What you need:** A web browser (Chrome, Edge, Firefox, or Safari), a [GitHub account](https://github.com/join) (free; confirm your email), and **write access** to this repository (you must be added as a collaborator). If you do not have write access, use the fork method described at the end of this section.

### 1. Open the project on GitHub

Go to: **<https://github.com/gauter/nordic-epub-evaluation>**

You will see a list of files. See the [Repository structure](#repository-structure) table for the full list and which file to edit for what (e.g. `SKILL.md` for workflow and report template, the checklist files for version-specific requirements).

### 2. Create a new branch (in the main repository)

1. Click the **branch selector** (it shows "main" or "master") at the top left above the file list.
2. Type a new branch name in the search/create field (e.g. `update-2025-1-requirement` or `fix-checklist-typo`). Use lowercase letters and hyphens; no spaces.
3. Click **"Create branch: [name] from 'main'"** (or the green button that creates the new branch). You are now working on this branch.

### 3. Find the right file

Click the filename to open it (e.g. `SKILL.md` or one of the checklist files).

### 4. Edit the file

1. Click the **pencil icon** ("Edit this file") at the top right of the file view.
2. The browser shows the file content in a text box. Use **Ctrl+F** (Windows/Linux) or **Cmd+F** (Mac) to search for the text you want to change.
3. Make your edits. Do not delete or change parts you are unsure about; when in doubt, ask.

### 5. Save your change (commit)

1. Scroll down to **"Commit changes"**.
2. In **"Commit message"**, write one short sentence describing what you changed (in English or your language).
3. **Important:** Leave **"Commit directly to the [your-branch-name] branch"** selected (do not choose main). That keeps your change on your branch.
4. Click the green **"Commit changes"** button.

### 6. Open a pull request (from your branch to main)

1. After the commit, a yellow bar often appears: **"Compare & pull request"**. Click it.
2. In the form: base = **main**, compare = your branch. Give the pull request a short title (e.g. "Update requirement X in 2025-1 checklist") and in the description write what you changed and why (1–3 sentences).
3. Click **"Create pull request"**.

### 7. After you have submitted

Someone with access to the repository will review and may comment or approve. To make further changes, edit the file again on the **same branch** and commit; the new commits will appear in the same pull request.

### 8. If you do not have write access to the main repository (fork)

1. Click **"Fork"** at the top right. You now work in your own copy (`github.com/[your-username]/nordic-epub-evaluation`).
2. In your fork, create a branch (same as step 2 above), edit and commit to that branch, then click **"Compare & pull request"** to open a pull request from your fork to the main repository’s `main` branch.

### 9. Important when changing content

- If you add or change a requirement in one of the checklists, check whether `SKILL.md` mentions that requirement (Quick reference table, phase descriptions, report template) and update it there if needed.
- Respect version boundaries: changes for 2015-1 only in the 2015-1 files, and similarly for 2020-1 and 2025-1. See [How to contribute](#how-to-contribute) for version boundaries.

## How to test the changes you just implemented

After you have edited the skill (on a branch or after it is merged), you can verify that the agent uses your updated text when it runs an evaluation.

**What you are testing:** That the skill applies your change (e.g. a new requirement in the checklist or report template) when the agent runs an evaluation.

**Prerequisite:** An **unzipped** EPUB that the agent can access—for example, open the folder containing the unzipped EPUB in Cursor, or give the agent the path. Prefer an EPUB you know (e.g. one with known issues that should be reported).

**Using "your" version of the skill:** If your change is on a branch and you want to test before merge, install the skill from that branch if your setup supports it (e.g. a branch URL); otherwise, test after the change is merged by reinstalling the skill from the main repository (run the same `npx skills add …` command from [Installation](#installation)).

**Running an evaluation:** In your agent (Cursor, Copilot, Claude, etc.), ask it to evaluate the unzipped EPUB folder using a prompt from [Commands and example prompts](#commands-and-example-prompts) (e.g. *"Run nordic-epub-evaluation on [path]"*).

**Checking the result:** Read the report the agent produces. Verify that (1) your change is reflected (e.g. the new requirement appears in Detailed findings or Summary), (2) the wording matches what you edited, and (3) the guideline version (2015-1, 2020-1, or 2025-1) and checklists used match what you changed.

**If something is wrong:** If the report does not reflect your change, confirm you have the correct version of the skill installed and that the EPUB you used actually exercises the part you changed (e.g. it has images if you changed image requirements).

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
