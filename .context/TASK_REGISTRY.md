# Central Task Registry & Collision Prevention Matrix
> **Master Coordinator for Snoopy Development**  
> **Rule Reference:** [.agents/rules/task_collision_prevention.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.agents/rules/task_collision_prevention.md)  
> **Policy:** All agents and developers MUST check this registry BEFORE modifying code to prevent merge collisions and duplicated effort.

---

## 1. Active & In-Flight Tasks

| Task ID | Feature / Description | Assigned To | Status | Target Files / Scope | Branch / Session | Started At | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| *(None currently active)* | Ready for next task | — | `IDLE` | — | — | — | All foundational rules and feature specs initialized. |

---

## 2. Completed Tasks Archive

| Task ID | Feature / Description | Completed By | Completed At | Final Commit / Pull Request | Summary |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TASK-001** | [Agent Operating Rules & Protocols](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/AGENTS.md) | `anshul_prajapati` | 2026-10-14 22:35 | Initial Rules Setup | Established foundational agent operating rules (dual-target architecture for standalone and Android Studio publishing, user prompt logging, collision prevention, feature blueprints, and session continuation protocols). |

---

## 3. Collision Detection & Merge Conflict Prevention Rules for Agents

When a user asks you to start or modify any task:

1. **Step 1: Check Target Files & Feature Scope**:
   - Look at the `Target Files / Scope` column in the Active Tasks table above.
   - If ANY file or feature directory overlaps with a task marked `IN_PROGRESS` by another user:
     - 🛑 **DO NOT EDIT OR OVERWRITE THE FILES SILENTLY.**
     - 📢 **IMMEDIATELY WARN THE USER**:
       > "⚠️ **TASK CONFLICT / MERGE RISK:** Task `<Task ID>` is currently being worked on by `<Assigned To>` in `<Target Files / Scope>`. Modifying these files will create Git merge conflicts!"
     - Ask the user whether to wait, create an isolated sub-branch, or coordinate with the other developer.

2. **Step 2: Register New Tasks**:
   - If the task is clear of conflicts or the user provides an isolated scope, append a new row to the **Active Tasks** table with status `IN_PROGRESS`.

3. **Step 3: Update Upon Completion**:
   - When a task is completed, move the row from **Active Tasks** to **Completed Tasks Archive** and set status to `COMPLETED`.
