# User Acceptance Testing (UAT) & Requirements Traceability Matrix (RTM)

## 1. Traceability Matrix Overview
This document validates that all functional and business requirements specified in the FRD are thoroughly verified against real-world user interaction workflows prior to final deployment.

| Req ID | User Story | Test Case ID | Test Focus | Expected Classification | Pass / Fail |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **FR-01** | US-01 (Natural Typing) | TC-UAT-01 | Organic Human Input | Likely Human-Written | Pass |
| **FR-01** | US-01 (Typing Velocity) | TC-UAT-02 | Unusually Fast Typing | Possibly AI-Assisted | Pass |
| **FR-03** | US-02 (Bulk Injection) | TC-UAT-03 | Single Large Paste Event | Possibly AI-Assisted | Pass |
| **FR-03** | US-02 (Threshold Override) | TC-UAT-04 | Multiple Paste Events (≥ 2) | Highly AI-Assisted | Pass |
| **FR-02** | US-01 (Session Logging) | TC-UAT-05 | SQLite Session Persistence | Record Logged to DB | Pass |

---

## 2. Detailed Test Cases

### Test Case ID: TC-UAT-01
* **Requirement Reference:** FR-01 (Organic User Composition)
* **Pre-condition:** User logged into HumanWrite editor interface.
* **Test Steps:**
  1. Navigate to `/editor`.
  2. Manually type a paragraph without using clipboard paste commands.
  3. Ensure natural pauses between words (average gap ~110–140 ms, typing speed ~35–50 WPM).
  4. Click **Analyze Writing**.
* **Expected Result:**
  * Output Label displays: `Likely Human-Written`.
  * Confidence score reflected with proper probability metric.
  * Session successfully committed to SQLite `sessions` table.
* **Actual Result:** Verified — Correctly classified as `Likely Human-Written`.
* **Status:** **PASS**

---

### Test Case ID: TC-UAT-02
* **Requirement Reference:** FR-01 (High Cadence Detection)
* **Pre-condition:** User logged into HumanWrite editor.
* **Test Steps:**
  1. Rapidly input characters with minimal latency (average gap < 60 ms, sustained speed > 130 WPM).
  2. Click **Analyze Writing**.
* **Expected Result:**
  * Output Label flags irregularity: `Possibly AI-Assisted` or `Highly AI-Assisted`.
* **Actual Result:** Model successfully identified anomalous keystroke velocity.
* **Status:** **PASS**

---

### Test Case ID: TC-UAT-03
* **Requirement Reference:** FR-03 (Single Clipboard Event)
* **Pre-condition:** Clipboard contains 150 words of pre-generated text.
* **Test Steps:**
  1. Open editor.
  2. Execute one paste action (`Ctrl + V`).
  3. Manually type 10 additional words.
  4. Click **Analyze Writing**.
* **Expected Result:**
  * System captures `paste_count = 1`.
  * Output Label displays: `Possibly AI-Assisted` with confidence > 70%.
* **Actual Result:** Verified — Real-time event handler tracked 1 paste event; confidence calibrated accurately.
* **Status:** **PASS**

---

### Test Case ID: TC-UAT-04
* **Requirement Reference:** FR-03 (Business Rule Override on Repeated Pastes)
* **Pre-condition:** Text editor initialized.
* **Test Steps:**
  1. Paste text once (`paste_count = 1`).
  2. Type 5 characters.
  3. Paste a second block of text (`paste_count = 2`).
  4. Click **Analyze Writing**.
* **Expected Result:**
  * Trigger hard business rule: If `paste_count >= 2`, force state to `Highly AI-Assisted` regardless of typing interval variance.
  * Confidence rating defaults to $\ge 80\%$.
* **Actual Result:** Verified — Hard rule executed, correctly categorized as `Highly AI-Assisted`.
* **Status:** **PASS**

---

### Test Case ID: TC-UAT-05
* **Requirement Reference:** FR-02 (Data Persistence & Historical Verification)
* **Pre-condition:** Completed analyses from TC-01 through TC-04.
* **Test Steps:**
  1. Click **View My Dashboard** (`/dashboard`).
  2. Inspect listed session entries.
* **Expected Result:**
  * Dashboard displays past session outputs, matching timestamps, and confidence percentages in chronological order.
* **Actual Result:** SQLite query executes seamlessly and renders all session rows correctly.
* **Status:** **PASS**
