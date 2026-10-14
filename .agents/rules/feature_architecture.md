# Rule: Feature Architecture & Workflow Blueprint Standard

## Purpose
Every feature developed in Snoopy must have a dedicated, single markdown file documenting its architecture, workflows, data models, and platform boundaries. This prevents ambiguous implementations, ensures consistency across contributors, and guarantees seamless support for both Standalone and Android Studio release builds.

## File Location Convention
Every feature must be placed in:
`c:/Users/anshul prajapati/OneDrive/Desktop/Snoopy/docs/features/<feature_name>.md`

## Standard Template
All feature documents must follow the structure defined in [TEMPLATE_FEATURE.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/docs/features/TEMPLATE_FEATURE.md).

## Mandatory Blueprint Sections

Each feature document must contain the following detailed sections:

1. **Feature Metadata & Objective**:
   - Feature Name & Code
   - Owner / Lead Contributor
   - Target Scam Vector (e.g. Phishing URL, Impersonation SMS, Advance-fee fraud)
   - User Benefit & Goal

2. **Architecture Blueprint**:
   - Component Breakdown (Core Engine, Presentation/UI, Platform Adapter)
   - Data Ingestion & Normalization
   - Heuristics, Signatures, or Machine Learning Model
   - Risk Scoring Methodology (0 to 100 confidence score + Red/Yellow/Green verdict)

3. **Workflow & Data Flow (Mermaid Diagram Required)**:
   - Visual flowchart of the analysis pipeline from input ingestion to verdict rendering.
   - User decision points and remediation steps (e.g., "Report Scam", "Block Sender", "Proceed Anyway").

4. **Dual-Target Execution Matrix**:
   - **Standalone Execution**:
     - How does the user trigger or test this feature in the standalone environment?
     - What platform capabilities are mocked or polyfilled?
   - **Android Studio & Google Play Build**:
     - Android OS APIs used (e.g., Android Share Sheet, NotificationListenerService, SMS BroadcastReceiver).
     - Required permissions in `AndroidManifest.xml`.
     - Google Play Policy adherence (e.g., Sensitive Permissions declarations, Privacy Policy compliance).

5. **File Mapping**:
   - Core files: `/core/...`
   - Standalone files: `/standalone/...`
   - Android files: `/android/...`
   - Test files: `/tests/...`

6. **Edge Cases, Errors & Privacy**:
   - Offline handling: Can the feature detect red flags without internet access?
   - Handling of false positives and false negatives.
   - PII protection: Sanitizing passwords, OTPs, or personal phone numbers before logging or querying external scam databases.
