# Business Requirements Document (BRD) — HumanWrite

## 1. Executive Summary & Problem Definition
Traditional plagiarism and AI detection systems evaluate linguistic distribution and perplexity. These approaches fail against rephrased or novel text generation. HumanWrite solves this by evaluating author behavioral dynamics during content composition to ensure authenticity in academic, assessment, and publishing workflows.

## 2. Business Objectives
- **Integrity Verification**: Provide educators and recruiters with verifiable proof of human authorship.
- **Process-Oriented Detection**: Detect bulk copy-paste injections and abnormal input cadences in real time.
- **Actionable Reporting**: Deliver transparent confidence ratings rather than opaque binary verdicts.

## 3. Scope Management (MoSCoW Prioritization)
- **Must Have**:
  - Client-side event capture (`avg_gap`, `paste_count`, `key_count`, `typing_speed`).
  - Real-time Flask endpoint delivering 3-tier classification.
  - Persistent SQLite session logging.
- **Should Have**:
  - Live AI probability graph during composition.
  - Historical dashboard summarizing past user scores.
- **Could Have**:
  - Granular token-level deletion analysis.
- **Won't Have (MVP)**:
  - Multi-tenant enterprise SSO and deep neural net transformer analysis.
