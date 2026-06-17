---
name: "Sensitive Information Protection"
description: "Protect sensitive information in code and configuration files. Never include usernames, home directories, or absolute paths that expose user identity."
applyTo: "**/{*.json,*.toml,*.yaml,*.yml,*.md,*.py,*.sh,*.bash}"
---

# Sensitive Information Protection Rules

## Never Include in Code or Config:
- **Usernames** in file paths (e.g., `/home/username/`)
- **Absolute paths** that expose user identity
- **Email addresses** or personal identifiers
- **API keys, tokens, or credentials** (use env vars instead)
- **IP addresses** of internal/private infrastructure
- **Database passwords** or connection strings with credentials

## What To Use Instead:

### Path Variables
- Use `${workspaceFolder}` for VS Code/MCP configs
- Use `$HOME` or `~` for shell scripts (will expand at runtime)
- Use relative paths (`.`, `..`, `./`) when possible
- Use environment variables for dynamic paths: `$PROJECT_ROOT`, `${PWD}`

### Credentials
- Reference `.env` files via settings modules
- Use environment variable fallbacks
- Document expected env vars in README
- Never hardcode secrets in config or code

### Example - BEFORE (❌ Bad):
```json
{
  "command": "cd /home/username/projects/sample-app && uv run python"
}
```

### Example - AFTER (✅ Good):
```json
{
  "command": "cd ${workspaceFolder} && uv run python"
}
```

## Configuration File Checklist:
- [ ] No absolute paths with usernames
- [ ] All paths use variables (`${workspaceFolder}`, `${HOME}`, etc)
- [ ] No credentials hardcoded
- [ ] Relative paths preferred where feasible
- [ ] Shell scripts use `~` or `$HOME` instead of `/home/username`

## When Reviewing Code:
- Scan for `/home/`, `/Users/` patterns with actual usernames
- Check `.vscode/`, `.env`, `config.json`, `mcp.json` files especially
- Use workspace variables for cross-machine compatibility
