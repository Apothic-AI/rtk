# Codex CLI Hooks

> Part of [`hooks/`](../README.md) — see also [`src/hooks/`](../../src/hooks/README.md) for installation code

## Specifics

- Programmatic Codex hook via `rtk hook codex`, wired through `hooks.json`
- `rtk init --codex` also enables `features.codex_hooks = true` in the active Codex `config.toml`
- `rtk init --codex` writes Codex hook configuration to the local `./.codex/` directory
- `rtk init -g --codex` writes to `$CODEX_HOME` when set, otherwise `~/.codex/`

## Behavior

- Codex `PreToolUse` hooks apply `updatedInput` to the pending Bash tool call.
- RTK uses transparent rewrite for Codex:
  - raw command: `git status`
  - hook response: `updatedInput.command = "rtk git status"`
  - Codex executes the RTK command and gets filtered output

This now matches the transparent rewrite behavior used by Claude Code and Cursor.
