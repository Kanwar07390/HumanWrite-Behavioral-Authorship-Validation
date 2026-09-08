# Functional Requirements Document (FRD) — HumanWrite

## 1. Functional Specifications
- **FR-01: Input Event Tracking**:
  - The editor must calculate typing speed (WPM) and key counts on `keyup`/`keydown` events.
  - The editor must intercept and record `paste` events and content length differences.
- **FR-02: Predictive Inference**:
  - The backend route `/analyze` must accept JSON payloads:
    `{"avg_gap": float, "paste_count": int, "key_count": int, "typing_speed": float}`.
  - Output must return classification state and numerical confidence.
- **FR-03: Edge Case Validation**:
  - If `paste_count >= 2`, system logic flags output as `Highly AI-Assisted` irrespective of typing intervals.

## 2. User Stories & Acceptance Criteria (Gherkin Syntax)

### US-01: Real-Time Input Evaluation
**As a** student or candidate,  
**I want** my writing session analyzed for natural human behavioral cadences,  
**So that** my independent authorship is verified transparently.

- **Scenario 1: Organic Human Composition**
  - **Given** an authenticated user is typing in the HumanWrite editor,
  - **When** keystroke intervals show irregular human variance and `paste_count == 0`,
  - **Then** the inference engine classifies the output as `Likely Human-Written` with confidence $\ge 80\%$.

- **Scenario 2: Bulk Content Injection**
  - **Given** content is populated via system clipboard actions,
  - **When** `paste_count >= 2`,
  - **Then** the system bypasses default linear scaling and tags the session as `Highly AI-Assisted`.
