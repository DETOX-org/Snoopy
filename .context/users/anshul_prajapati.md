# Contributor Intent & Prompt Log: Anshul Prajapati
> **Username:** `anshul_prajapati`  
> **Git Identity:** `Anshul Prajapati <anshulprajapati2220@gmail.com>`  
> **Role:** Lead Architect / Project Owner  
> **Repository:** Snoopy (DETOX)

---

## Session History & Prompts

### [2026-10-14 22:20:00] Session 1: Foundational Agent Operating Rules & Multi-Target Framework Setup

#### 1. User Prompt (Verbatim):
> *"hey make a agaent rule or agaent should follow these step*  
> *we are making both standalone app and app which will be published and converted into an app after doing all things by the android studio*  
> *and the agent shouls write all the things and prompts and what user trying to explain in a single md file with the username*  
> *and if anyone is taking or doing any task which is still under some one task or the prompts or anything they do where it store it will match and firstly tell the other user who are doing the same task and tell it will not merge or it will get code merge*  
> *and also make a every single file for the features how the workflow and architecture should be for every feature*  
> *and also when some one doing any task create a context file for the session with theri name so if they get back and go to and tell thyey can continue from there*  
> *now make this rules"*

#### 2. User Intent & Detailed Explanations:
1. **Dual-Target Application Strategy**:
   - The user explained that Snoopy is not just a standard web/desktop tool or just a mobile app—it is both.
   - It needs to be developed as a standalone app (testable independently) AND converted/bundled through Android Studio for publication (Google Play store ready).
   - The agent must be instructed to never write code that breaks either target; separation between core scam logic and Android Studio native wrappers is essential.

2. **Personalized Prompt & Discussion Logging**:
   - The user wants every prompt, requirement, and thought they explain to be preserved in a dedicated markdown file labeled with their username (`.context/users/<username>.md`).
   - This ensures full context tracking, eliminates lost instructions, and documents contributor thoughts.

3. **Collision Detection & Code Merge Prevention**:
   - In a multi-developer or multi-agent environment, tasks often overlap, leading to duplicated effort or severe Git merge conflicts.
   - The user explicitly requested a mechanism where tasks and ongoing work are recorded and matched.
   - Before any user or agent touches a task or file already being handled by someone else, the agent MUST immediately alert the user that a collision exists, explain the merge risk, and prevent accidental overwrites.

4. **Per-Feature Architecture & Workflow Specifications**:
   - The user mandated that every single feature must have its own dedicated markdown file in `docs/features/`.
   - Each feature file must comprehensively specify how the feature functions, its end-to-end workflow, data flow, and architecture across both standalone and Android Studio environments.

5. **Session Continuation & Context Resumption**:
   - When a user works on a task and takes a break or leaves, the agent must generate and maintain a session context file (`.context/sessions/<username>_session.md`).
   - When the user returns, they can seamlessly resume work from the exact checkpoint without re-explaining anything.

#### 3. Key Decisions & Artifacts Created:
- [x] Defined master rules in [AGENTS.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/AGENTS.md) and [GEMINI.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/GEMINI.md).
- [x] Created modular rule specifications under [.agents/rules/](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.agents/rules/):
  - [dual_target_architecture.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.agents/rules/dual_target_architecture.md)
  - [user_logging.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.agents/rules/user_logging.md)
  - [task_collision_prevention.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.agents/rules/task_collision_prevention.md)
  - [feature_architecture.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.agents/rules/feature_architecture.md)
  - [session_continuation.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.agents/rules/session_continuation.md)
- [x] Created central task tracking matrix: [.context/TASK_REGISTRY.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.context/TASK_REGISTRY.md).
- [x] Created feature architecture templates and baseline specs under [docs/features/](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/docs/features/).
- [x] Initialized active session context: [.context/sessions/anshul_prajapati_session.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.context/sessions/anshul_prajapati_session.md).

---
