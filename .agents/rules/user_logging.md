# Rule: User-Specific Prompt & Intent Logging Protocol

## Purpose
To preserve complete team memory, prevent loss of context across conversations, and understand the motivations and explanations of each user/contributor, every interaction must be logged into a dedicated markdown file per username in `.context/users/<username>.md`.

## Target File Location
`c:/Users/anshul prajapati/OneDrive/Desktop/Snoopy/.context/users/<username>.md`

## Username Detection Procedure
When starting a session or receiving a prompt:
1. Check if the user stated their name or handle in chat.
2. Otherwise, check Git configuration: `git config user.name`.
3. Otherwise, check system environment variable: `$env:USERNAME` (Windows) or `$USER` (Linux/macOS).
4. Sanitize the username into lowercase `snake_case` (e.g., `Anshul Prajapati` -> `anshul_prajapati`).

## What to Log
For every interaction or task, the agent must log:
1. **Timestamp**: ISO 8601 or local date and time.
2. **User's Raw Prompt / Request**: Exactly what the user asked.
3. **User Intent & Rationale**: What the user was trying to achieve or explain in their own words.
4. **Architectural & Design Constraints**: Constraints mentioned by the user (e.g., "must run in Android Studio", "no external heavy frameworks", etc.).
5. **Decisions Agreed Upon**: Technical decisions made during the turn.
6. **Task / Features Impacted**: Links to relevant files in `docs/features/`.

## Logging Format Example

```markdown
## [2026-10-14 22:30:00] Session: <Session Title or Feature Name>

### User Prompt:
> "<Exact or summarized user prompt>"

### User Intent & Explanation:
- The user explained that ...
- The core problem being addressed is ...
- Specific preferences requested: ...

### Key Decisions & Agreed Scope:
- [x] Decision 1: ...
- [x] Decision 2: ...

### Artifacts Touched / Created:
- [docs/features/<feature>.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/docs/features/<feature>.md)
- [.context/sessions/<username>_session.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.context/sessions/<username>_session.md)

---
```

## Critical Rules
- **NEVER OVERWRITE EXISTING LOG ENTRIES**: Always append to the bottom of the user's file.
- **Maintain a Table of Contents**: If the file grows long, maintain a session summary table at the top.
