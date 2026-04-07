# DEV_AGENT_PROMPT — project-noemi/ai-fluency-hu

> **Hungarian AI Fluency course** — bilingual (HU/EN) educational content built with **MkDocs Material** for static site generation, **LaTeX** templates for pamphlet PDFs, and **Python** scripts for content processing. 12 course modules per language covering the NoéMI 4D framework (Delegation, Description, Discernment, Diligence).

---

## 1. Orientation — Read the Docs

Before touching any file, read and internalise:

| Document | Why |
|----------|-----|
| `README.md` | Project overview and content structure |
| `mkdocs.yml` | MkDocs Material configuration — site name, theme, plugins, extensions |
| `requirements.txt` | Python dependencies: mkdocs, mkdocs-material, pymdown-extensions |
| `course/localization_plan.md` | Translation strategy and localization guidelines |
| `docs/localization_guidelines.md` | Detailed localization rules |
| `docs/INDEX.md` | Documentation index |
| `docs/static_site_generation.md` | How the MkDocs site is built |
| `docs/latex_maintenance.md` | LaTeX template maintenance guide |
| `includes/` | Shared Markdown includes (abbreviations, feedback, license) |

### Tech Stack

- **MkDocs Material 9+** for static site generation
- **Python 3** scripts for content processing
- **LaTeX** templates for pamphlet PDF generation (`course/templates/pamphlet_template.tex`)
- **pymdown-extensions** for enhanced Markdown (abbreviations, etc.)
- Bilingual content: `course/hu/` (Hungarian) and `course/en/` (English)

### Key Patterns

- **Course structure**: 12 modules per language in `course/{lang}/`:
  - `01` — Introduction to AI Fluency
  - `02` — The AI Fluency Framework
  - `03` — Deep Dive 1: What is Generative AI
  - `04` — Delegation
  - `05` — Applying Delegation
  - `06` — Description
  - `07` — Deep Dive 2: Effective Prompting Techniques
  - `08` — Discernment
  - `09` — The Description-Discernment Loop
  - `10` — Diligence
  - `11` — Conclusion and Certificate
  - `12` — Additional Activities
- **Hungarian is primary**: `course/hu/` is the source of truth; `mkdocs.yml` points to `course/hu/`
- **Includes**: `includes/abbreviations.md`, `includes/feedback-hu.md`, `includes/license-hu.md` — shared across pages
- **LaTeX pamphlets**: `course/templates/pamphlet_template.tex` — compiled via `scripts/compile_pamphlets.sh`
- **Scripts**: Python and Bash utilities in `scripts/`:
  - `build-docs.sh` — build MkDocs site
  - `start-server.sh` — local dev server
  - `compile_pamphlets.sh` — LaTeX → PDF compilation
  - `convert_pdfs_to_images.py` — PDF → image conversion
  - `extract_pdf_text.py` — PDF text extraction
  - `get_transcript.py` — transcript processing
  - `pamphlet_translation_analysis.py` — translation quality analysis
  - `rename_pamphlets.sh` — file renaming utility
- **Custom theme**: `course/hu/custom_theme/` directory for MkDocs overrides
- **Custom CSS**: `course/hu/custom.css` for styling overrides
- **`.clinerules`** — AI assistant rules file (respect its contents)

---

## 2. Plan — Write a Plan

Before writing code, create a plan in `docs/IMPLEMENTATION_PLAN.md`:

1. **What** — new module, content update, tooling change, or translation
2. **Language scope** — HU only, EN only, or both
3. **Module impact** — which of the 12 modules are affected
4. **LaTeX impact** — does the pamphlet template need updating?
5. **MkDocs impact** — navigation, plugins, or extension changes?
6. **Translation parity** — ensure HU and EN stay aligned

---

## 3. Documentation — Write User Docs First

- Course content **is** the documentation — write module content first
- Update `docs/localization_guidelines.md` if changing translation conventions
- Update `course/localization_plan.md` for translation status tracking
- Maintain `docs/INDEX.md` as the master reference
- Add abbreviations to `includes/abbreviations.md` for consistent terminology

---

## 4. Tests — Write Tests First

No formal test framework, so focus on:

- **MkDocs build**: `mkdocs build` must complete without errors or warnings
- **Link check**: All internal links between modules resolve
- **LaTeX compilation**: `scripts/compile_pamphlets.sh` must produce valid PDFs
- **Translation parity**: Both `course/hu/` and `course/en/` have matching module files
- **Abbreviation check**: All terms in `includes/abbreviations.md` are used consistently
- **Python scripts**: Run each script with `--help` or test data to verify functionality

---

## 5. Code — Write the Code

### Course Content Rules

- **Hungarian modules**: proper Hungarian typography (á, é, í, ó, ö, ő, ú, ü, ű)
- **English modules**: natural English, pedagogically appropriate
- Follow the NoéMI 4D framework terminology consistently
- Use MkDocs Material admonitions for tips, warnings, examples
- Reference images with relative paths
- Include abbreviation definitions in `includes/abbreviations.md`

### MkDocs Rules

- `mkdocs.yml` is the single source of configuration — `docs_dir: course/hu`
- Navigation structure mirrors the 12-module sequence
- Use `pymdown-extensions` features (abbreviations, details, tabs) for rich content
- Custom theme overrides in `course/hu/custom_theme/`
- Privacy plugin enabled — respect content restrictions

### LaTeX Rules

- Pamphlet template: `course/templates/pamphlet_template.tex`
- Compile via `scripts/compile_pamphlets.sh` — do not manually run `pdflatex`
- Test with both HU and EN content
- Ensure Hungarian hyphenation package is loaded (`\usepackage[hungarian]{babel}`)

### Python Script Rules

- Python 3.9+ compatible
- Use `requirements.txt` dependencies only
- Scripts must be runnable standalone (`if __name__ == '__main__'`)
- Handle file encoding explicitly (`encoding='utf-8'`) — Hungarian characters

---

## 6. Test the Code — Verify Everything

```bash
pip install -r requirements.txt     # Install Python dependencies
mkdocs build                        # Build MkDocs site
mkdocs serve                        # Local dev server
scripts/compile_pamphlets.sh        # Compile LaTeX pamphlets
python scripts/convert_pdfs_to_images.py  # Test PDF conversion
```

- MkDocs build must have zero warnings
- All 12 modules render correctly in browser
- LaTeX pamphlets compile without errors
- Hungarian characters display correctly throughout
- Navigation works for all modules

---

## Branch Workflow

```
feature/* ──► develop ──► main
```

- All work on `feature/*` branches off `develop`
- PR to `develop` for review
- `develop` → `main` via PR only (enforced by CI)
