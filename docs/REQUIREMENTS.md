# Requirements — project-noemi/ai-fluency-hu

> Canonical specification for the AI Fluency Hungarian course project. This document is the primary source of truth for what needs to be built, validated, and maintained. All PRs and implementation plans should reference requirements defined here.

---

## 1. Project Overview

The AI Fluency Hungarian (MI Fluencia Keretrendszer) project is a bilingual (HU/EN) educational course built with MkDocs Material for static site generation, LaTeX templates for pamphlet PDFs, and Python scripts for content processing. The course covers 12 modules teaching the NoéMI 4D Framework (Delegation, Description, Discernment, Diligence) for effective AI collaboration.

### 1.1 Target Users

- Hungarian-speaking learners seeking practical AI collaboration skills.
- Educators and trainers delivering AI fluency workshops.
- Organizations adopting the NoéMI 4D Framework for team AI readiness.
- English-speaking learners (via the parallel English translation).

### 1.2 Design Principles

- **Bilingual parity**: Hungarian is the primary language; English follows as a parallel translation. Both must stay synchronized.
- **Static site delivery**: All course content is served as a static MkDocs Material site — no backend required.
- **Declarative configuration**: `mkdocs.yml` is the single source of truth for site structure, navigation, and extensions.
- **Reproducible builds**: A developer should be able to build and serve the site with only Python and pip installed.
---

## 2. Functional Requirements

### FR-1: Course Content Structure

| ID | Requirement | Status |
|----|-------------|--------|
| FR-1.1 | The course MUST consist of 12 modules per language, following the defined curriculum sequence. | Implemented |
| FR-1.2 | Hungarian modules MUST reside in `course/hu/` and serve as the primary source of truth. | Implemented |
| FR-1.3 | English modules MUST reside in `course/en/` and maintain structural parity with the Hungarian version. | Implemented |
| FR-1.4 | Each module MUST be a standalone Markdown file named with a zero-padded numeric prefix. | Implemented |
| FR-1.5 | The course MUST include a `kurzus-anyagok.md` (Course Materials) page as supplementary content. | Implemented |

### FR-2: Static Site Generation (MkDocs)

| ID | Requirement | Status |
|----|-------------|--------|
| FR-2.1 | The site MUST be built using MkDocs with the Material theme. | Implemented |
| FR-2.2 | `mkdocs.yml` MUST define `docs_dir: course/hu` to serve the Hungarian content as the primary site. | Implemented |
| FR-2.3 | The `nav` section in `mkdocs.yml` MUST list all 12 modules plus the Course Materials page in the correct sequence. | Implemented |
| FR-2.4 | `mkdocs build` MUST complete with zero errors and zero warnings. | Not verified |
| FR-2.5 | The site MUST use the Material theme with Hungarian (`hu`) language configuration. | Implemented |
| FR-2.6 | The site MUST include custom CSS (`custom.css`) and custom JavaScript (`js/abbreviations-first-only.js`). | Implemented |
| FR-2.7 | The site MUST use a custom theme directory (`course/hu/custom_theme`) for template overrides. | Implemented |
### FR-3: MkDocs Extensions and Plugins

| ID | Requirement | Status |
|----|-------------|--------|
| FR-3.1 | The `abbr` Markdown extension MUST be enabled for abbreviation support. | Implemented |
| FR-3.2 | The `admonition` extension MUST be enabled for tips, warnings, and examples. | Implemented |
| FR-3.3 | The `pymdownx.snippets` extension MUST auto-append `includes/abbreviations.md` to every page. | Implemented |
| FR-3.4 | The `privacy` plugin MUST be enabled to respect content restrictions. | Implemented |

### FR-4: Shared Includes

| ID | Requirement | Status |
|----|-------------|--------|
| FR-4.1 | Common abbreviations MUST be defined in `includes/abbreviations.md` and shared across all pages. | Implemented |
| FR-4.2 | Feedback includes (`includes/feedback-hu.md`) MUST be available for Hungarian pages. | Implemented |
| FR-4.3 | License includes (`includes/license-hu.md`) MUST be available for Hungarian pages. | Implemented |
| FR-4.4 | The `watch` directive in `mkdocs.yml` MUST monitor the `includes/` directory for live reload. | Implemented |

### FR-5: LaTeX Pamphlet System

| ID | Requirement | Status |
|----|-------------|--------|
| FR-5.1 | A shared LaTeX template MUST exist at `course/templates/pamphlet_template.tex`. | Implemented |
| FR-5.2 | The `scripts/compile_pamphlets.sh` script MUST compile all pamphlets from LaTeX to PDF without errors. | Not verified |
| FR-5.3 | The template MUST load the Hungarian hyphenation package (`\usepackage[hungarian]{babel}`). | Implemented |
| FR-5.4 | Pamphlet source files MUST reside in `course/hu/pamphlets/` for Hungarian content. | Implemented |
### FR-6: Utility Scripts

| ID | Requirement | Status |
|----|-------------|--------|
| FR-6.1 | `scripts/build-docs.sh` MUST build the MkDocs site. | Implemented |
| FR-6.2 | `scripts/start-server.sh` MUST start a local MkDocs development server. | Implemented |
| FR-6.3 | `scripts/compile_pamphlets.sh` MUST compile LaTeX pamphlets to PDF. | Implemented |
| FR-6.4 | `scripts/convert_pdfs_to_images.py` MUST convert PDFs to image format. | Implemented |
| FR-6.5 | `scripts/extract_pdf_text.py` MUST extract text content from PDF files. | Implemented |
| FR-6.6 | `scripts/get_transcript.py` MUST process video transcripts. | Implemented |
| FR-6.7 | `scripts/pamphlet_translation_analysis.py` MUST analyze translation quality between HU and EN pamphlets. | Implemented |
| FR-6.8 | `scripts/rename_pamphlets.sh` MUST provide a file renaming utility. | Implemented |
| FR-6.9 | All Python scripts MUST be compatible with Python 3.9+ and handle UTF-8 encoding explicitly. | Implemented |
| FR-6.10 | All Python scripts MUST be runnable standalone (`if __name__ == '__main__'`). | Not verified |

### FR-7: Cookie Consent and Analytics

| ID | Requirement | Status |
|----|-------------|--------|
| FR-7.1 | The site MUST display a cookie consent dialog with accept and manage options. | Implemented |
| FR-7.2 | Analytics MUST use a custom provider configured in `mkdocs.yml`. | Implemented |
| FR-7.3 | GitHub cookies MUST be configurable and enabled by default. | Implemented |

### FR-8: Content Editing Support

| ID | Requirement | Status |
|----|-------------|--------|
| FR-8.1 | The site MUST provide edit links pointing to the GitHub repository (`edit/main/course/hu/`). | Implemented |
| FR-8.2 | The `content.action.edit` feature MUST be enabled in the Material theme. | Implemented |
---

## 3. Non-Functional Requirements

### NFR-1: Content Quality

| ID | Requirement | Status |
|----|-------------|--------|
| NFR-1.1 | Hungarian modules MUST use proper Hungarian typography (á, é, í, ó, ö, ő, ú, ü, ű). | Implemented |
| NFR-1.2 | English modules MUST use natural, pedagogically appropriate English. | Implemented |
| NFR-1.3 | All content MUST follow the NoéMI 4D framework terminology consistently. | Implemented |
| NFR-1.4 | The Hungarian version MUST use informal tone ("te" form) for learner engagement. | Implemented |

### NFR-2: Localization

| ID | Requirement | Status |
|----|-------------|--------|
| NFR-2.1 | Translation conventions MUST be documented in `docs/localization_guidelines.md`. | Implemented |
| NFR-2.2 | Translation status MUST be tracked in `course/localization_plan.md`. | Implemented |
| NFR-2.3 | Both `course/hu/` and `course/en/` MUST have matching module files for structural parity. | Not verified |

### NFR-3: Build Reproducibility

| ID | Requirement | Status |
|----|-------------|--------|
| NFR-3.1 | All Python dependencies MUST be listed in `requirements.txt` with minimum version constraints. | Implemented |
| NFR-3.2 | The project MUST build successfully with only Python 3.8+, pip, and a LaTeX distribution installed. | Implemented |
| NFR-3.3 | Dependencies MUST be limited to: `mkdocs>=1.5.0`, `mkdocs-material>=9.0.0`, `pymdown-extensions>=10.0.0`. | Implemented |
### NFR-4: Maintainability

| ID | Requirement | Status |
|----|-------------|--------|
| NFR-4.1 | Project documentation MUST be maintained in the `docs/` directory with `docs/INDEX.md` as the master reference. | Implemented |
| NFR-4.2 | LaTeX maintenance procedures MUST be documented in `docs/latex_maintenance.md`. | Implemented |
| NFR-4.3 | Static site generation procedures MUST be documented in `docs/static_site_generation.md`. | Implemented |
| NFR-4.4 | Images MUST use relative paths within Markdown files. | Implemented |

---

## 4. Integration Requirements

### IR-1: GitHub Ecosystem

| ID | Requirement | Status |
|----|-------------|--------|
| IR-1.1 | The repository MUST be hosted under the `project-noemi` GitHub organization. | Implemented |
| IR-1.2 | A GitHub Actions CI/CD workflow MUST deploy the MkDocs site to GitHub Pages. | Implemented |
| IR-1.3 | A workflow MUST enforce the `develop`-to-`main` PR flow. | Implemented |

### IR-2: Branch Workflow

| ID | Requirement | Status |
|----|-------------|--------|
| IR-2.1 | All work MUST be done on `feature/*` branches off `develop`. | Enforced |
| IR-2.2 | PRs MUST target `develop` for review before merging. | Enforced |
| IR-2.3 | The `develop` → `main` merge MUST be done via PR only (enforced by CI). | Implemented |
---

## 5. Current Status and Implementation Gaps

### 5.1 Implemented and Stable

All core functional requirements (FR-1 through FR-8) are implemented. The project delivers a fully functional bilingual AI Fluency course with MkDocs Material static site generation, LaTeX pamphlet compilation, and utility scripts for content processing.

### 5.2 Known Gaps and Future Considerations

| Area | Gap | Priority |
|------|-----|----------|
| Testing | No automated test suite exists. MkDocs build validation and link checking should be automated in CI. | High |
| Translation parity | No automated check to verify `course/hu/` and `course/en/` module files remain structurally aligned. | Medium |
| Dependency pinning | `requirements.txt` uses minimum version constraints (`>=`) rather than exact pins, which may lead to build inconsistencies. | Medium |
| Script testing | Python scripts lack unit tests and `--help` documentation is not verified. | Medium |
| LaTeX CI | Pamphlet compilation is not integrated into CI — failures are only caught manually. | Medium |
| Accessibility | No accessibility audit of the generated site has been performed. | Low |
| Search | MkDocs search plugin is not configured — content discovery relies on navigation only. | Low |

---

## 6. Acceptance Criteria

A contribution or release is considered complete when:

1. All modified or newly added functional requirements pass manual verification.
2. `mkdocs build` completes with zero errors and zero warnings.
3. LaTeX pamphlets compile without errors (if pamphlet content was modified).
4. Hungarian and English module files maintain structural parity.
5. Documentation in `docs/` is updated to reflect any changes.
6. The `DEV_AGENT_PROMPT.md` workflow (plan, document, test, code, verify) has been followed.
7. The branch workflow (`feature/*` → `develop` → `main`) has been respected.

---

## Revision History

| Date | Author | Change |
|------|--------|--------|
| 2026-04-09 | Dev Agent | Initial creation based on repository analysis (closes #2) |
