# HumanWrite — Web-Based Behavioral Authorship Validation

HumanWrite addresses the limitations of standard text-matching and linguistic AI detectors by analyzing **how** content is authored rather than solely analyzing static text output. By capturing client-side behavioral dynamics—keystroke timing, cadence variations, and paste actions—the platform uses a machine learning classifier to identify AI-assisted writing in real time.

## Key Features & BA Artifacts
- **Behavioral Feature Extraction**: Captures raw client-side metrics (`avg_gap`, `paste_count`, `key_count`, `typing_speed`).
- **Real-Time Classification Engine**: Scikit-Learn `Pipeline` running `StandardScaler` and `LogisticRegression` exposed through a lightweight Flask REST API.
- **Three-Tier Output State**: Dynamically renders classifications:
  - `Likely Human-Written`
  - `Possibly AI-Assisted`
  - `Highly AI-Assisted` (supplemented with probability confidence metrics).
- **Session History Persistence**: SQLite backend tracking historical submission scores and behavioral timestamps.

## Tech Stack
- **Frontend**: HTML5, CSS3, JavaScript (Real-time keystroke/event tracking)
- **Backend API**: Python, Flask, Flask-CORS
- **Machine Learning**: Scikit-learn, Pandas, NumPy, Joblib
- **Database**: SQLite3

## System Architecture & Data Flow
1. User writes content within the interactive web editor.
2. Client-side script calculates keystroke intervals, typing velocity (WPM), and paste events.
3. Payload is dispatched via `POST /analyze` to the Flask application.
4. Feature vectors are normalized and passed through the serialized model pipeline.
5. The API returns classification predictions and confidence ratings stored in `sessions.db`.

## Documentation
- [Business Requirements Document (BRD)](docs/BRD_HumanWrite.md)
- [Functional Requirements Document (FRD)](docs/FRD_HumanWrite.md)
- [System Architecture & Data Design](docs/System_Architecture.md)
