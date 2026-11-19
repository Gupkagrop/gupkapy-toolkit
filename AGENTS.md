# Project Operational Guidelines (AGENTS.md)

> [!NOTE]
> **Назначение файла:** Контракт правил и архитектурных стандартов для агентов в библиотеке `gupkapy-toolkit`.
> Агент считывает этот файл автоматически при открытии рабочей области.

## 1. Project Overview & Tech Stack
- **Project Name:** `gupkapy-toolkit`
- **Target Platform:** Python Library (Cross-platform)
- **Runtime:** Python >= 3.12 (CPython 3.12, 3.13, 3.14)
- **Package Manager & Tooling:** `uv`
- **Git Remote:** `origin` (`https://github.com/Gupkagrop/gupkapy-toolkit.git`)
- **Main Branch:** `main`

## 2. Standard Commands (Harness Sensors)
- **Install Dependencies:** `uv sync`
- **Run Tests:** `uv run pytest`
- **Linter & Code Style:** `uv run ruff check .`
- **Build Distribution:** `uv build`

## 3. Session Continuity & Orientation Protocol
- **Every new chat/task MUST start with:**
  1. `git status` and `git log -n 5 --oneline` (review recent commit history).
  2. Reading `TASK.md` in repository root to determine active phase, backlog, and decisions.
  3. Checking `ROADMAP.md` for feature and module milestone status.
  4. Reading `repomix-output.xml` (or regenerating via `npx repomix --compress` if stale).

## 4. Coding & Architecture Standards
- **Language & Comments:** All code symbols in English. All docstrings, inline comments, and annotations strictly in Russian.
- **Strict Typing:** Every function signature and class attribute must include explicit type hints (`typing.Any` is strictly prohibited). Use generics (`TypeVar`, `Generic`, `[T]`).
- **Complexity & Flat Flow:** Adhere to early returns (maximum nesting depth $\le 3$).
- **Single Responsibility:** Keep functions within 30-40 lines; break down complex logic into private helpers (`_helper_func`).
- **Zero Placeholders:** Never commit mocks, placeholders, or `TODO` markers. Every component must be 100% production-ready.
- **Secrets Protection:** Zero hardcoded credentials or tokens.

## 5. Pre-Commit Checklist
- [ ] Automated tests run and pass green (`uv run pytest`).
- [ ] Static analyzer passes with zero warnings (`uv run ruff check .`).
- [ ] `TASK.md` updated with completed milestone and commit hash.
- [ ] Conventional Commit authored in Russian (e.g., `feat: ...`, `chore: ...`).
- [ ] Push commits to remote: `git push origin main`.
