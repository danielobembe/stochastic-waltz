# CLAUDE.md
## Stochastic Waltz — Instructions for Claude Code

---

## Start Here

Before doing anything else, read the Project Brief:
**`docs/01-options-blog-project-brief.md`**

It describes what this project is, the full technical stack, and the current development status. The Project Brief also points to four supporting documents — read whichever are relevant to the current phase before starting work:

1. **`docs/02-options-blog-design-brief.md`**
2. **`docs/03-options-blog-technical-spec.md`**
3. **`docs/04-options-blog-development-plan.md`**
4. **`docs/05-options-blog-file-structure.md`**

---

## Behavioral Instructions

- **Always ask before creating files or folders** not listed in the File & Folder Structure document
- **Always ask before installing packages** not listed in `requirements.txt`
- **Never use `venv`** — the Python environment manager is conda; ask the user for the environment name if not already created
- **Never make changes to more than one document or file at a time** without confirming with the user first
- **Always propose changes and wait for approval** before editing any existing document
- **Flag deviations** — if something in the project requires departing from the Design Brief, Technical Specification, or File & Folder Structure, flag it explicitly and explain why before proceeding
- **Update phase status** — at the end of each completed phase, update the Current Status table in `options-blog-project-brief.md` to mark the phase as done before closing the session

---

## Working Style

- **Propose before acting** — before making any change (creating a file, editing code, running a command), describe what you plan to do and why, then wait for explicit confirmation before proceeding
- **One action at a time** — describe and confirm each action individually; do not bundle multiple changes into a single step without prior agreement
- **Confirm understanding** — if a request is ambiguous, restate your interpretation and ask for confirmation before doing anything

---

## Current Phase

Check the Project Brief (`options-blog-project-brief.md`) for the current development phase and status before starting any session.

---

*End of CLAUDE.md*
