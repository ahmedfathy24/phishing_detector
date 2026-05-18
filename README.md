# PhishGuard v2 — Intelligent URL Phishing Detection System

![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![Chrome Extension](https://img.shields.io/badge/Chrome_Extension-4285F4?style=for-the-badge&logo=google-chrome&logoColor=white)

PhishGuard v2 is a state-of-the-art phishing detection platform that combines behavioral analysis with machine learning to protect users from malicious web threats. It features a premium "cyber-themed" interface, a robust backend, and a real-time browser extension for seamless protection.

##  System Architecture
PhishGuard v2 follows a **decoupled architecture**, ensuring a clean separation of concerns between the logic engine, the user interface, and the browser integration. 

| Component | Technology Stack | Responsibility |
| :--- | :--- | :--- |
| **Backend** | FastAPI, Scikit-learn, Pandas | Feature extraction, ML inference, and REST API |
| **Frontend** | HTML5, Vanilla JS, CSS3 | Real-time UI updates, Data visualization, and Local state |
| **Extension** | Chrome Extensions API, JS | Real-time active tab scanning and seamless browser integration |

##  Advanced Machine Learning Features

###  Core Detection Model
The heart of PhishGuard v2 is a highly trained **Random Forest** classifier. To achieve high accuracy, the system relies on a custom-built feature extractor that evaluates **41 distinct numerical features** from any given URL. This deep inspection covers structural anomalies, lexical characteristics, and suspicious token combinations to effectively differentiate between benign and malicious links.

###  Lookalike / Typosquatting Detection Engine
A core strength of PhishGuard v2 is its dedicated engine for detecting "Lookalike" domains used in brand impersonation attacks. The system employs a **normalization logic** that strips away common obfuscation techniques:

- **Character Normalization**: The engine maps visual similarities to their likely intended characters:
  - `0` → `o` | `1` → `l` | `3` → `e` | `5` → `s`
  - `7` → `t` | `8` → `b` | `9` → `g` | `@` → `a`
  - `rn` → `m` (e.g., `rnicrosoft.com` is flagged as a match for `microsoft`)
- **Fuzzy Matching**: Uses `SequenceMatcher` to calculate similarity scores between normalized domains and registered brand labels.
- **Smart Logic**: Legitimate brand domains (e.g., `paypal.com`) are correctly identified as safe, while malicious variations (e.g., `paypa1.com`) trigger a high-risk alert.

##  Real-Time Browser Extension
PhishGuard v2 extends its protection directly to your browser. The custom-built extension communicates seamlessly with the local FastAPI backend to provide:
- **Real-Time Automated Shield**: Intercepts browser navigations globally to instantly halt malicious connections.
- **Intelligent Fallback**: Re-routes malicious attempts securely using the `webNavigation` API directly to a local, isolated warning page (`blocked.html`).

##  Dynamic Dataset Explorer & Local History
- **API-Driven Explorer**: The frontend fetches the `dataset.csv` directly from the backend via a REST API endpoint (`/api/dataset`), ensuring the UI always reflects the current training set with real-time filtering.
- **Local Scan History**: Utilizes **Browser LocalStorage** to maintain a persistent, private record of scan results across browser sessions without the need for a database.

## 📂 Project Structure
```text
phishguard_v2/
├── backend/                # Logic & ML Service
│   ├── app.py              # FastAPI Entry Point
│   ├── data/               # Training Datasets (dataset.csv)
│   ├── models/             # Serialized ML Models (.pkl)
│   └── src/                # Feature Extraction & Training logic
├── frontend/               # Presentation Layer
│   ├── phishguard_v2.html  # Main UI
│   ├── style.css           # Premium Cyber-style Styling
│   └── script.js           # Frontend Logic & API Interaction
├── PhishGuard_Extension/   # Browser Integration Shield
│   ├── manifest.json       # Extension Configuration & CSP
│   ├── background.js       # Core real-time interception logic
│   ├── blocked.html        # Premium isolated warning page
│   ├── popup.html          # Extension UI Dashboard
│   └── popup.css/.js       # Extension UI Logic & Styling
└── README.md               # Presentation-Ready Documentation
```

## Setup & Deployment

### Prerequisites
Python 3.8+ installed on your system.

### 1. Install Dependencies
Open your terminal and run the following command to install the necessary Python packages:

```bash
pip install fastapi uvicorn scikit-learn pandas
```

### 2. Launch the Backend API
Navigate to the backend directory and start the FastAPI server:

```bash
cd backend
python app.py
```
*(Alternatively, you can run: `uvicorn app:app --reload`)*
The API will be available at `http://localhost:8000`.

### 3. Launch the Frontend UI
In a separate terminal, navigate to the frontend directory and start a local web server:

```bash
cd frontend
python -m http.server 5500
```
Access the application at: `http://localhost:5500/phishguard_v2.html`

### 4. Install the Browser Extension Shield
1. Open Google Chrome or Microsoft Edge and navigate to `chrome://extensions/`.
2. Enable **Developer mode** (usually a toggle in the top right corner).
3. Click **Load unpacked** and select the `PhishGuard_Extension/` directory from this project.
4. Accept the permissions, and pin the PhishGuard extension to your toolbar. The background shield is now active!

---
*PhishGuard v2 — Intelligent Detection. Premium Protection.*
