# Active Session Contexts Directory
> **Rule Reference:** [.agents/rules/session_continuation.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.agents/rules/session_continuation.md)

This directory stores real-time session context snapshots for every contributor (`<username>_session.md`).

## How Session Continuation Works

1. **While Working**:
   - The agent updates the user's session file with completed subtasks, files touched, architectural decisions, and the next immediate step.

2. **When Returning**:
   - The user can simply state: *"Resume my session"* or *"What were we doing?"*.
   - The agent reads `<username>_session.md`, checks git status, reports what was accomplished, and immediately offers or triggers the next concrete step.

3. **Collision Checking**:
   - Other users/agents read this directory along with `.context/TASK_REGISTRY.md` to see which tasks and files are currently occupied, preventing merge collisions.
