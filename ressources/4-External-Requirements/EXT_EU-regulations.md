---
id: EXT_EU-regulations
category: external_requirements
title: European Union regulation to comply
obligation: MUST
requirement_references: [CRA, IAA, RGPD, ENISA, EAA]
internal_references: []
normative_vs_informative: normative
---

# IAA - EU IA Act
The law splits all artificial intelligence into four distinct risk categories, dictating what is banned and what requires heavy compliance
- **Unacceptable Risk (Banned)**
  - Completely prohibited in the EU. This includes real-time biometric tracking in public, AI that infers emotions in the workplace or schools, social scoring by governments, untargeted scraping of facial images to build databases, and subliminal manipulation.
- **High Risk (Heavily Regulated)**
  - Permitted but subject to strict pre-market and post-market controls. This covers AI used in critical infrastructure, medical devices, educational grading, recruitment/HR software, credit scoring, and law enforcement.
- **Limited Risk (Transparency Focus)**
  - Systems like chatbots or generative AI (e.g., image generation tools or text summarizers) must explicitly notify users that they are interacting with an AI. AI-generated text or media must contain cryptographic watermarks or synthetic markers.
- **Minimal Risk (Unregulated)** 
  - Broad applications like spam filters or AI in video games have no additional obligations under the Act.

# CRA - EU Cyber Resilient Act
The CRA (Regulation 2024/2847) focuses on cybersecurity for "products with digital elements." 
- **"Secure by Default" Engineering**
  - Software cannot hit the EU market with known exploitable vulnerabilities. Default configurations must be locked down tight.
- **Strict Access Control & Identity Mandates**
  - Annex I explicitly targets generic or shared secrets. Applications must utilize proper identity and access management systems, secure session boundaries (from login to automatic logout), and mandatory Multi-Factor Authentication (MFA).
- **Cryptographic Enforcement**
  - Requires state-of-the-art encryption for data both at rest and in transit. This reinforces why legacy auth protocols are discarded in favor of modern, cryptographically signed frameworks (like JWS/JWT profiles).
- **CE Marking Requirement**
  - Compliant software and hardware products must carry a visible CE mark to prove they meet the EU’s essential security standards.

# NIS2 - Network and Information Security
NIS 2 eliminates inconsistencies between EU member states by creating strict, harmonized cybersecurity baselines.
- **Mandatory "State-of-the-Art" Security**
  - Forces covered entities to implement modern cryptographic protocols, continuous vulnerability scanning, and multi-factor authentication (MFA) across all digital boundaries.
    - **RFC7636** : OIDC-PKCE enforced
    - **RFC9068** : Access by JWT audience strict
- **Supply Chain Security**
  - Requires organizations to hold their software vendors to strict cybersecurity standards, making secure-by-design architectures a commercial necessity.
- **Personal Executive Liability**
  - Management bodies and executives can be held personally liable and temporarily suspended from managerial duties if their organization systematically fails to address critical cyber vulnerabilities.

# GDPR - General Data Protection Regulation
The GDPR focuses entirely on data protection principles, transparency, and consumer sovereignty over personal information.
- **Security of Processing (Article 32)**
  - Dictates that companies must use appropriate technical controls. For modern apps, this implies banning legacy authentication.
    - **RFC9700** : Forbid 'implicit flow'
    - **RFC9068** : Access by JWT to reduce personnal data exposed
- **Data Minimization**
  - Mandates that only data necessary for the immediate transaction should be collected. In authorization architectures, this translates to utilizing pseudonymized access token scopes rather than passing full user details inside open payloads.
- **Data Breach Notification**
  - Enforces a strict 72-hour window to report data breaches to supervisory authorities (like CNIL in France) if personal data is exposed.

# eIDAS 2 - Electronic Identification, Authentication and Trust Services
eIDAS 2 updates the old 2014 framework by creating a unified, cross-border digital identity ecosystem for European citizens.
- **The EUDI Wallet**
  - Mandates that member states provide citizens with a decentralized European Digital Identity Wallet. Users can securely store credentials, identities, digital signatures, and medical/tax records.
- **Acceptance Requirements**
  - Large online platforms (like Amazon or Meta) and public entities are legally obligated to accept the EUDI wallet for identity verification (AuthN).
- **Standardized Identity Architecture**
  - Relies on standardized OpenID Connect (OIDC) profiles to allow seamless, cross-border authentication without forcing citizens to use separate corporate login systems.

# DORA - Digital Operational Resilience Act
DORA standardizes digital risk management specifically for the financial sector to protect the broader economic system from cascading technology failures.
- **Five Pillars of Resilience**
  - Mandates strict programs across ICT risk management, incident reporting, operational resilience testing, third-party risk governance, and threat intelligence sharing.
- **Third-Party Oversight**
  - Broadens enforcement power to directly monitor core ICT service providers (like AWS, Azure, or critical SaaS vendors) that service European banks.
- **Rigorous Penetration Testing**
  - Enforces advanced threat-led penetration testing (TLPT) to ensure software applications cannot be compromised by authorization bypasses or architectural flaws.
    - OIDC Core 1.0
    - RBAC applicatif

# EAA - European Accessibility Act
The EAA (Directive (EU) 2019/882) is a historic digital inclusion law. Its strict compliance deadline went live on June 28, 2025, forcing companies selling physical or digital products in the EU to guarantee equal access for people with disabilities.
- **Technical Baseline (EN 301 549 & WCAG 2.2)** 
  - Web apps and mobile PWAs are legally mandated to align with WCAG 2.2 Level AA accessibility standards. This includes supporting screen-reader compatibility, strict text contrast minimums (4.5:1), and full keyboard-only navigation.
- **Broad Digital Scope**
  - It directly hits e-commerce websites/apps, banking systems, passenger transport apps, e-books, smartphones, and smart TVs.
- **CE Marking Requirement**
  - Accessible digital physical products (like payment terminals or smartphones) must carry a visible CE mark and have fully documented technical folders proving accessible development.
- **Exemptions & Penalties** 
  - Only microenterprises (<10 employees and ≤€2M turnover) are exempt from service-level compliance.
