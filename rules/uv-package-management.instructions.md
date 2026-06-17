---
description: "Use when: managing Python packages, installing dependencies, adding or removing packages, updating pyproject.toml, or maintaining uv.lock files. Requires uv for dependency management."
name: "UV Package Management"
applyTo: "**/{pyproject.toml,uv.lock,uv_*.lock,requirements*.txt,*.py}"
---
# UV Package Management

- Use `uv` for Python package management and dependency installation in this repository. Treat this as a hard rule unless the user explicitly asks for another tool.
- Add runtime dependencies with `uv add <package>` and development-only dependencies with `uv add --dev <package>`.
- Remove dependencies with `uv remove <package>`.
- Sync or install existing dependencies with `uv sync`; avoid `pip install -r requirements.txt` unless the user explicitly asks for pip compatibility work.
- Keep `pyproject.toml` and the relevant `uv.lock` file in sync when dependencies change.
- If a dependency must come from a custom index or platform-specific source, prefer configuring it through `pyproject.toml` and `uv` rather than ad hoc install commands.