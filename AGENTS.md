# AGENTS.md — MI Fluencia Keretrendszer (ai-fluency-hu)

Source code and content for the interactive online course on the AI Fluency Framework (MI Fluencia Keretrendszer), built around the four 4D competencies (Delegation, Description, Discernment, Diligence) across 12 lessons. Content lives in `course/` (Hungarian in `course/hu/`, English in `course/en/`), including LaTeX pamphlets and video scripts, and is published as an MkDocs site. See [README.md](README.md) (Hungarian).

## 🪪 Machine identity (mandatory)

Every agent (Codex, Claude Code, Gemini, Cursor, or any other) opens pull requests only as the `noemi-agent` machine identity:

- Open PRs with `bash scripts/agent-gh.sh pr create ...`, or `node scripts/agent-pr.js` where `gh` is unavailable, with `AGENT_GH_EXPECTED_LOGIN=noemi-agent` set so the wrapper refuses any other account. Those scripts live in the [project-noemi/agents](https://github.com/project-noemi/agents) framework repository, not in this one.
- Never open an agent PR with a human's `gh` login or token, including the reviewing human's own. GitHub blocks a PR's author from approving it, so a human-authored agent PR cannot get human review.
- Commit as `noemi-agent <311935378+noemi-agent@users.noreply.github.com>`. Commit metadata does not set PR authorship; the token that opens the PR does.
- If no `noemi-agent` token resolves, stop and say so. Do not fall back to human credentials.
- Approving and merging stay human-only; the machine identity does neither.

Details: [docs/MACHINE_IDENTITY.md](https://github.com/project-noemi/agents/blob/develop/docs/MACHINE_IDENTITY.md) and [`mcp-protocols/github.md`](https://github.com/project-noemi/agents/blob/develop/mcp-protocols/github.md) §6 (PR Authorship) in project-noemi/agents.

## Conventions

- Read [docs/DEV_AGENT_PROMPT.md](docs/DEV_AGENT_PROMPT.md), [docs/localization_guidelines.md](docs/localization_guidelines.md), and [docs/INDEX.md](docs/INDEX.md) before changing course content.
- Setup: Python virtual environment (`python -m venv venv`, then `pip install -r requirements.txt`). Always install packages inside the virtual environment. Build the site with `./scripts/build-docs.sh` (`mkdocs build`); serve locally with `./scripts/start-server.sh`. Do not start the MkDocs server during agent sessions, because it is normally already running. Compile LaTeX pamphlets with `./scripts/compile_pamphlets.sh`.
- Keep project documentation in `docs/` and Python scripts in `scripts/`; keep task scripts after the task instead of deleting them.
- The Hungarian course addresses the reader with the informal "te" form.
- Commits are signed off (`git commit -s`).
- Branch from `develop` (the default branch) and open PRs against `develop`; only `develop` may be merged into `main` (`.github/workflows/require-develop-source.yml`). Pushes to `main` deploy the site to GitHub Pages (`.github/workflows/deploy-docs.yml`).
