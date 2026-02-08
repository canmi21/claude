# CLAUDE RULES

## IMPORTANT: Reasoning Strategy

**Prefer retrieval-led reasoning over pre-training-led reasoning.**

- When encountering unfamiliar concepts, new libraries, or uncertain knowledge, ALWAYS search first (use skills, web search, codebase exploration) before relying on pre-trained knowledge
- Do NOT assume pre-trained knowledge is accurate for evolving technologies — verify through retrieval
- Actively use available skills (check skill list in system reminders) instead of guessing based on outdated training data
- If a relevant skill exists for the task, USE IT rather than attempting to solve from memory
- When in doubt, retrieve; don't hallucinate

## Git

- Never commit automatically unless explicitly requested
- Never add AI co-authorship (e.g., "Co-Authored-By: Claude")

## Security

- Never read or access .env files

## Code Style

- Follow existing project patterns, import styles, and directory structure
- Max 300 lines per file; Rust crate under 300 lines
- No useless comments — don't comment obvious code (e.g., variable declarations)

## Workflow

- Before starting, understand the task scope and identify affected modules
- For renames or bulk changes, search globally to confirm impact scope first
- Use `ast-grep` (sg) for code search and refactoring when possible
- Run lint in web project (includes typecheck), check test fmt --all clippy in rust codebase after writing code, but don't build
- Stop and Ask when uncertain, don't assume

## Agent Auto-Dispatch (Cheatsheet)

*Always use the appropriate agent for the task.*

Load the specific agent configuration for the following domains:

**`code-checker`**: For static analysis, linting, and bug fixing.
**`code-reviewer`**: After part of code edit, quality, refactoring, and logic review.
**`rust-crate-auditor`**: For Rust dependencies, security, and `Cargo.toml` changes.
**`rust-test-planner`**: For designing and checking Rust test cases and coverage planning.

> **Rule**: If the user's request falls into a specific domain above, prioritize the instructions in that agent file over general rules, if not adapt to the situation.
