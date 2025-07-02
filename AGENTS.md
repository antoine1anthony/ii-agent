# AGENTS.md

This AGENTS.md provides AI agents with the context and conventions needed to work effectively within the **ii-agent** repository.

---

## 1. Scope & Precedence

1. **Purpose**: Human-authored guidance that AI agents must parse before touching any source files.
2. **Scope**: Applies to the entire `ii-agent` repository.
3. **Precedence Rules**:
   - **Highest**: Direct instructions from user prompts or system messages.
   - **Next**: This AGENTS.md at the repository root.
   - **Lowest**: Default AI heuristics.

---

## 2. Project Structure

```
ii-agent/
├── docs/                   # User-facing documentation
│   └── usage.md
├── src/                    # Core Python packages
│   └── ii_agent/
│       ├── __init__.py
│       ├── core.py         # Agent orchestration logic
│       ├── tools.py        # Tool definitions
│       └── utils.py        # Helper functions
├── tests/                  # Unit and integration tests
│   └── test_core.py
├── examples/               # Example configurations and demos
│   └── simple_run.py
├── Dockerfile              # Container build recipe
├── docker-compose.yml      # Orchestration for local dev
├── pyproject.toml          # Build & dependency management
├── README.md               # Overview and installation
└── AGENTS.md               # This file
```

**Agent Note**: Focus modifications within `src/ii_agent` and add new modules under that namespace.

---

## 3. Coding Conventions

- **Language**: Python 3.10+
- **Formatting**: Use **Black** (`black .`) and **isort** (`isort .`) for import sorting.
- **Linting**: Follow **Flake8** (`flake8 src/ tests/`). Enforce a maximum line length of **88**.
- **Typing**: All public functions and methods require Python type hints. Use `from __future__ import annotations`.
- **Docstrings**: Use Google-style docstrings. Every module, class, and function must have a docstring.

---

## 4. Dependency Management

- **Installation**: `pip install .` or `pip install -e .` for development.
- **Locking**: Dependencies managed via `pyproject.toml`; refrain from editing `poetry.lock` by hand.
- **Updating**: Run `poetry update` and review changes before committing.

---

## 5. Testing & CI

- **Unit Tests**: Run `pytest --maxfail=1 --disable-warnings -q` in project root.
- **Coverage**: Enforce at least **90%** coverage across `src/ii_agent`. Use `pytest --cov=ii_agent`.
- **Continuous Integration**:
  - **GitHub Actions** defined in `.github/workflows/ci.yml`.
  - Steps include linting, type-check, testing, and coverage reporting.

**Agent Requirement**: Any code change must pass CI pipeline without modifications.

---

## 6. Docker & Local Development

- **Build**: `docker build -t ii-agent:dev .`
- **Run**: `docker-compose up --build`
- **Shell Access**: `docker-compose run --service-ports app bash`
- **Environment**: Set variables via `.env.example` and copy to `.env`.

---

## 7. Pull Request Guidelines

- **Branch Naming**: `feature/<short-description>`, `bugfix/<short-description>`.
- **Commit Messages**: Use imperative mood, e.g., `Add caching to core module`.
- **PR Title**: Brief summary; include issue number if applicable, e.g., `#42: Support async tool calls`.
- **Review Checklist**:
  1. All tests pass.
  2. Linting and formatting complete.
  3. Docstrings added/updated.
  4. No secrets or large binaries.

---

## 8. Agent Behavior Protocols

1. **Read-Only Phase**: Always run project linter and tests in a dry-run mode (`--check`) before proposing code.
2. **Patch Generation**: Provide a unified patch via the repository root; do not scatter minor fixes across multiple commits.
3. **Validation**: After generating code, run full test suite and lint checks programmatically; abort if any errors.
4. **Documentation**: For any new feature or public API change, update `docs/usage.md` and inline docstrings.
5. **Examples**: Add or extend example scripts under `examples/` demonstrating the new functionality.

---

*End of AGENTS.md*

