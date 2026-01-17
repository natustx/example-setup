# Global Rules

## Code
- Read files before changing them
- NEVER use placeholders or omit code
- Use best practice libraries and frameworks; don't reinvent the wheel
- Follow existing project patterns
- Follow KISS, YAGNI, and DRY principles
- Small files (<350 lines), single responsibility
- Prefer composition over inheritance
- Comments should ONLY explain the code, not the change history
- Use specific exceptions with context in error messages but no sensitive data

## Web Testing
- NEVER start up any dev servers yourself unless testing the startup code
- First check if the web server is running, if not ask the user

## General
- Be brutally honest about whether an idea is good or bad
- NEVER do git adds or git commits unless the user instructs you to
- Tests & lints must pass before completing work
- “Mac Mini” => SSH there; find hosts/IPs via `tailscale status`

## Security
- Never put secrets in code - use environment variables
- Never commit .env files
- Validate all external inputs at system boundaries
- Sanitize inputs before storing / processing
- Validate auth tokens server-side
- Never log tokens, passwords, or personal data

## Logging
- Use correlation IDs across service boundaries
- Structured JSON logs with: timestamp, level, correlation_id, event
- Single source of truth for each piece of state

## CLI Commands
- <important>Single-line commands ONLY - no backslash (`\`) line continuations</important>
- Avoid `!=` operator (bash escapes `!`). Use truthy checks: `select(.x)` or `select(.x == val | not)`
- When calling tools from the shell, follow this rubric:
  - File reads: `bat`
  - Find files: `fd`
  - Find text: `rg`
  - Read directory: `eza`
  - Directory trees:  `eza --tree --level=N`
  - Find code structure (TS/TSX): `ast-grep` (default `--lang ts` or `--lang tsx` for React)
    - `.ts` → `ast-grep --lang ts -p '<pattern>'`
    - `.tsx` → `ast-grep --lang tsx -p '<pattern>'`
    - For other languages, set `--lang` appropriately (e.g., `--lang rust`)
  - Narrow matches interactively by piping results to `fzf`
  - Inspect JSON with `jq`
  - Inspect YAML / XML with `yq`
  - Git: `git <command>` (only use `git -C <dir> <command>` if you need to inspect a separate repo)

## Project Commands
- Use Taskfile. Standard commands to always use:
  - `task setup`, don't run `uv pip install`, `npm install`
  - `task lint`, don't directly call linters
  - `task dev`
  - `task test`, don't directly invoke tests

## Git
- Keep `main` branch at repo root. Worktrees for feature branches, in `.worktrees/`
- Ue `wt` for worktree/branch management

  ```bash
  wt switch -c feature-name   # Create new worktree + branch
  wt switch feature-name      # Switch to existing worktree
  wt list                     # Show all worktrees
  wt merge                    # Squash-merge to main, cleanup
  wt remove                   # Remove current worktree
  ```

# Python

- Use `uv` for package management
- Use `pyproject.toml` with minimal info
- Use `ruff` for linting and formatting (not black)
- Type hints for public APIs; Pydantic for validation

# TypeScript

- Use `pnpm` for package management
- Minimal `package.json`
- Prefer `unknown` over `any`; use strict mode
- Named exports over default exports
- async/await over raw promises
- Promise.all for parallel operations

## Plan Mode

- Make the plan extremely concise. Sacrifice grammar for the sake of concision.
- At the end of each plan, give me a list of unresolved questions to answer, if any.