---
id: EXT_INT-cyber
category: external_requirements
title: Cyber requirment to comply and justify any gap
obligation: MUST
requirement_references: [OWASP,ASVS,SCVC,SAMM,ANSSI,EISA,CISA,NIST]
internal_references: []
normative_vs_informative: normative
---

# OWASP - Open Worldwide Application Security Project
- **A01: Broken Access Control**
  - This remains the top threat. Applications fail to properly check user permissions on the backend, allowing authorization bypasses (e.g., a standard user accessing admin APIs).
  - Compliancy impact : NIS2 & DORA
- **A02: Security Misconfiguration**
  - Rising significantly in severity, this covers running applications with default credentials, unhardened cloud environments, or overly verbose error messages that leak internal infrastructure data.
  - Compliancy impact : NIS2 & CRA
- **A03: Software Supply Chain Failures**
  - Highlighting third-party dependency risks, this covers malicious open-source packages, compromised build tools, or untrusted third-party plug-ins embedded directly into code.
  - Compliancy impact : CRA
- **A04: Cryptographic Failures**
  - Focuses on data-in-transit or data-at-rest protection issues, such as using outdated cipher suites, insecure hashing algorithms, or mishandling symmetric encryption keys.
  - Compliancy impact : GDPR & NIS2
- **A05: Injection**
  - Classic exploits—like SQL injection, Cross-Site Scripting (XSS), or newer Prompt Injection threats in applications utilizing Large Language Models (LLMs)—where user-supplied input is directly executed as commands.
  - Compliancy impact : GDPR & DORA
- **06: Vulnerable and Outdated Components**
  - This vulnerability occurs when your software relies on third-party, open-source libraries, frameworks, or dependencies that contain known, publicly disclosed security flaws (CVEs).
  - Compliancy impact : NIS2 & CRA
- **A07: Identification and Authentication Failures**
  - This category covers architectural and functional flaws in how your application confirms a user's identity, manages active sessions, and protects authentication routes.
  - Compliancy impact : NIS2 & DORA
- **A08: Software and Data Integrity Failures**
  - This vulnerability occurs when code and critical infrastructure accept software updates, data payloads, or serialized objects from untrusted sources without verifying their cryptographic signatures or structural validity.
  - Compliancy impact : CRA
- **A09: Security Logging and Monitoring Failures**
  - This is an operational vulnerability where the application fails to log critical security events, stores logs insecurely, or lacks active monitoring and real-time alerting.
  - Compliancy impact : NIS2 & GDPR
- **A10: Server-Side Request Forgery (SSRF)**
  - SSRF occurs when a web application fetches a remote resource (such as a profile picture, web hook, or configuration file) from a URL provided directly by a user, without validating that destination URL first.
  - Compliancy impact : NIS2 & DORA

# OWASP ASVS - Application Security Verification Standard
Provides the exact technical checklist your engineering team needs to design and build secure software.
- **Actionable Blueprints**
  - It features granular, verifiable requirements (e.g., "Verify that all code-verifier challenges use SHA-256 hashing during the OAuth process").
- **Tiered Security Levels**
  - It maps your code structure across three distinct compliance levels:
    - **Level 1 (Opportunistic):**
      - Standard consumer apps; verifiable entirely through automated scanning (SAST/DAST).
    - **Level 2 (Standard):** 
      - Enterprise, B2B, or financial applications handling sensitive data; requires architecture reviews and threat modeling.
    - **Level 3 (Advanced):** 
      - High-assurance, critical infrastructure, or medical applications where a compromise poses significant risks.

# OWASP SCVS - Software Component Verification Standard
To satisfy the EU Cyber Resilience Act's software security requirements, development teams use the OWASP SCVS to identify and systematically reduce risks within their supply chains.
- **Software Bill of Materials (SBOM)**
  - Mandates generating a machine-readable bill of materials (e.g., using CycloneDX formats) to map out every library, framework, and transitive dependency shipped inside your application.
- **Build Environment Hardening**
  - Verifies the security of your continuous integration and deployment pipelines (CI/CD) to prevent unauthorized attackers from injecting malicious code during compilation.
- **Provenance Tracking**
  - Establishes verification points to mathematically prove the integrity of packages, ensuring third-party tools haven't been modified upstream.

# OWASP SAMM - Software Assurance Maturity Model
If you want to transition from simply fixing bugs to building an established enterprise security department, the OWASP SAMM framework evaluates your organizational maturity across five core operational functions:
- **Governance:**
  - Measuring how well your team manages strategy, compliance obligations, and security training programs.
- **Design:**
  - Standardizing how your product managers and architects evaluate security requirements and handle early threat modeling before code is written.
- **Implementation:**
  - Governing secure build mechanisms, automated code scanning tools, and secret management patterns.
- **Verification:**
  - Organizing architecture reviews, automated penetration testing routines, and bug bounty initiatives.
- **Operations:**
  - Mapping out incident response timelines, legacy environment decommissioning protocols, and operational patch management.

# ANSSI - Agence Nationale de la Sécurité des Systèmes d'Information
For a software editor building and deploying a Progressive Web App (PWA), ANSSI’s mandates are grouped into key technical and operational requirements:
- **Architectural Isolation: The BFF Pattern**
  - ANSSI strongly advises against storing raw cryptographic tokens (Access/Refresh Tokens) directly in browser-accessible storage (like localStorage or sessionStorage) due to Cross-Site Scripting (XSS) risks.
    - **The Mandate**
      - You must implement a Backend-for-Frontend (BFF) architecture.
    - **How it works**
      - The PWA frontend communicates with a lightweight, first-party backend proxy using secure, encrypted, HTTP-only, SameSite=Strict cookies. The BFF backend handles the complex OIDC-PKCE workflow, holds the tokens securely, and appends them to API requests out of the browser's reach.
- **PWA Browser Layer Hardening**
  - Because a PWA runs directly in the client's browser, you must restrict the execution environment using strict browser security headers.
    - **Content Security Policy (CSP)**
      - Implement a robust CSP header (prohibiting 'unsafe-inline' and 'unsafe-eval') to stop XSS vectors from stealing session data or manipulating the DOM.
    - **Service Worker Protection**
      - ANSSI requires verifying the integrity of the PWA Service Worker. The Service Worker script must be served with explicit Cache-Control: no-store headers and use Subresource Integrity (SRI) hash checks to ensure it has not been modified in transit.
    - **Local Storage Enclosure**
      - If the PWA caches business data locally via IndexedDB or Cache API for offline capabilities, that data must be minimized and cryptographically isolated. Sensitive personal information should never be cached permanently on the user's local disk.
- **Identity and Session Management**
  - ANSSI aligns with global standards but adds strict enforcement rules for authentication pathways:
    - **Multi-Factor Authentication (MFA)**
      - Mandatory for administrative paths and strongly enforced for regular users. ANSSI explicitly prefers FIDO2/WebAuthn standards (biometrics, security keys) over SMS-based OTPs.
    - **Session Lifespans**
      - Tokens and sessions must be short-lived. The app must implement automatic, absolute session timeouts (e.g., 15 minutes of inactivity) that wipe both the backend session and the frontend PWA application state.
- **Code Lifecycle and Supply Chain Sovereignty**
  - As a software editor, ANSSI evaluates your development pipeline to prevent upstream software supply chain contamination.
    - **Vulnerability Remediation Tracking**
      - Editors must maintain a documented patch management program ensuring critical vulnerabilities (CVEs) in third-party npm or backend packages are patched within days of discovery.
    - **SBOM and Reproducible Builds**
      - You must generate a verified Software Bill of Materials (SBOM) and ensure your build pipeline is deterministic, preventing arbitrary code injection during the build process.

# EISA

# CISA

# NIST

# HIPAA
