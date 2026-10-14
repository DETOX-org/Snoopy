# SNOOPY AGENT OPERATING RULES & PROTOCOLS

Please see the authoritative master rules in [AGENTS.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/AGENTS.md).

All agents working on this project must strictly comply with:
1. **Dual-Target Architecture**: Seamless compatibility with both the Standalone application and the Android Studio published application.
2. **User Intent & Prompt Logging**: Mandatory append-only logging to [.context/users/<username>.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.context/users/).
3. **Task Collision & Merge Conflict Prevention**: Mandatory check of [.context/TASK_REGISTRY.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.context/TASK_REGISTRY.md) before writing any code to prevent simultaneous overlapping edits.
4. **Per-Feature Architecture & Workflow Blueprints**: Every feature must have its own architecture file in [docs/features/<feature_name>.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/docs/features/).
5. **Session Continuation Context**: Dedicated resumption state in [.context/sessions/<username>_session.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/.context/sessions/).
