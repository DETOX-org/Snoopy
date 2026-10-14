# Feature Specification: Check Suspicious Links
> **Feature ID:** `FEAT-002`  
> **Status:** `ACTIVE`  
> **Lead / Owner:** `DETOX Core Team`  
> **Target Release:** Standalone & Android Studio  
> **Parent Architecture:** [standalone_vs_android_architecture.md](file:///c:/Users/anshul%20prajapati/OneDrive/Desktop/Snoopy/docs/features/standalone_vs_android_architecture.md)

---

## 1. Executive Summary & Objective

The **Check Suspicious Links** engine analyzes web URLs and hyperlinks to identify phishing sites, fraudulent payment gateways, credential harvesting portals, and malicious redirects before a user navigates to them.

### Core Attack Vectors Evaluated:
- **Typosquatting & Lookalike Domains**: E.g., `paypa1.com`, `arnazon.com`, `apple-security-check.net`.
- **Deceptive Subdomain Stacking**: E.g., `bankofamerica.com.login-verify-account.top`.
- **Suspicious Top-Level Domains (TLDs)**: Unusually high abuse-rate TLDs commonly associated with disposable phishing campaigns.
- **Raw IP Address URLs**: E.g., `http://192.168.1.1/secure/login`.
- **Excessive Path / Query Deception**: Obfuscated base64 query strings, misleading anchor tags, and deceptive redirect parameters (`redirect_to=`, `dest=`).
- **Punycode / Homograph Attacks**: Cyrillic or non-Latin glyphs masquerading as standard ASCII characters (e.g., `xn--...`).

---

## 2. Architecture & Link Inspection Pipeline

```mermaid
graph TD
    RawURL[Raw Link / URL Input] --> Canonicalizer[URL Parser & Canonicalizer]
    Canonicalizer --> DomainExtractor[Extract Protocol, Subdomain, Apex Domain, TLD, Path]
    DomainExtractor --> PunycodeDetector[Detect Homograph & Punycode]
    DomainExtractor --> TyposquatMatcher[Compare against Popular Brand Lexicons (Levenshtein)]
    DomainExtractor --> SubdomainChecker[Analyze Subdomain Depth & Target Brands in Subdomains]
    DomainExtractor --> TLDAnalyzer[Check TLD Reputation Database]
    
    PunycodeDetector --> Aggregator[URL Risk Aggregator]
    TyposquatMatcher --> Aggregator
    SubdomainChecker --> Aggregator
    TLDAnalyzer --> Aggregator
    
    Aggregator --> Output[Safety Score, Deconstruction Report & Safe Alternative Suggestion]
```

---

## 3. Workflow & User Journey

1. **Submission**:
   - *Standalone*: User enters or pastes URL into the link inspection search bar.
   - *Android App*: User long-presses a link in an SMS, WhatsApp message, or browser, selects "Share", and chooses **Snoopy Check Link**.
2. **Safe Parsing (Non-Executing)**:
   - Snoopy **NEVER** automatically renders or navigates to the target page directly on the user's primary browser.
   - It performs passive structural analysis and metadata querying.
3. **Deconstruction View**:
   - Snoopy reveals the **actual destination domain** in clear, bold typography, stripping out deceptive subdomains so the victim sees who actually owns the site.
   - Example: For `https://paypal.com.verify-billing.tk/`, Snoopy highlights:
     > *"Actual Destination Domain: **verify-billing.tk** (NOT PayPal)"*
4. **Actionable Recommendations**:
   - "Do not enter login credentials or bank details."
   - "If you were expecting this company, visit `https://paypal.com` directly in your browser."

---

## 4. Dual-Target Execution Matrix

| Capability | Standalone Application | Android Studio Published App |
| :--- | :--- | :--- |
| **Input Source** | Web link form, URL parameter query (`?url=...`) | Android Intent Filter for `http`/`https` URLs & Text sharing |
| **Domain Lookups** | Browser-safe domain heuristics & bundled offline DB | Bundled SQLite database of top 10,000 legitimate domains for instant offline typosquat detection |
| **Link Preview** | Non-executing static preview & DNS report | Custom Chrome Tabs / Isolated WebView for safe sandboxed inspection (optional) |
| **Permissions** | Standard Web permissions | `android.permission.INTERNET` |

---

## 5. Security & Privacy
- **URL Parameter Stripping**: Strips tracking tokens (e.g. `utm_*`, `fbclid`) to preserve user privacy before evaluating URLs.
- **Passive Safety**: No automatic downloads or cookie acceptance when evaluating links.
