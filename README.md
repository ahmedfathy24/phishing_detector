# PhishGuard v2 — Intelligent URL Phishing Detection System

PhishGuard v2 is a state-of-the-art phishing detection platform that combines behavioral analysis with machine learning to protect users from malicious web threats. It features a premium "cyber-themed" interface and a robust, scalable backend.

##  System Architecture
PhishGuard v2 follows a **decoupled architecture**, ensuring a clean separation of concerns between the logic engine and the user interface. This modularity allows for independent scaling and maintenance of the detection service and the presentation layer.

| Component | Technology Stack | Responsibility |
| :--- | :--- | :--- |
| **Backend** | FastAPI, Scikit-learn, Pandas | Feature extraction, ML inference, and REST API |
| **Frontend** | HTML5, Vanilla JS, CSS3 | Real-time UI updates, Data visualization, and Local state |

##  Advanced Machine Learning Features

###  Lookalike / Typosquatting Detection Engine
A core strength of PhishGuard v2 is its dedicated engine for detecting "Lookalike" domains used in brand impersonation attacks. The system employs a **normalization logic** that strips away common obfuscation techniques used by attackers:

- **Character Normalization**: The engine maps visual similarities to their likely intended characters:
  - `0` → `o` | `1` → `l` | `3` → `e` | `5` → `s`
  - `7` → `t` | `8` → `b` | `9` → `g` | `@` → `a`
  - `rn` → `m` (e.g., `rnicrosoft.com` is flagged as a match for `microsoft`)
- **Fuzzy Matching**: Uses `SequenceMatcher` to calculate similarity scores between normalized domains and registered brand labels.
- **Smart Logic**: Legitimate brand domains (e.g., `paypal.com`) are correctly identified as safe, while malicious variations (e.g., `paypa1.com`) trigger a high-risk alert.

### 📊 Dynamic Dataset Explorer
The system features a live explorer for the training data, served dynamically via a **REST API endpoint** (`/api/dataset`).
- **API-Driven**: Instead of hardcoding data, the frontend fetches the `dataset.csv` directly from the backend, ensuring the UI always reflects the current training set.
- **Real-time Filtering**: Users can search and filter through thousands of records by URL or label (Legitimate vs Phishing).

### Local Scan History
To provide a seamless user experience, PhishGuard v2 utilizes **Browser LocalStorage** to maintain a persistent record of scan results. 
- **Persistence**: Your history is saved across browser sessions without the need for a database.
- **Privacy**: All scan history remains local to your browser, ensuring data privacy.

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
└── README.md               # Presentation-Ready Documentation
```

## ⚙️ Setup & Deployment

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
*The API will be available at `http://localhost:8000`.*

### 3. Launch the Frontend UI
In a separate terminal, navigate to the frontend directory and start a local web server:
```bash
cd frontend
python -m http.server 5500
```
*Access the application at: **[http://localhost:5500/phishguard_v2.html](http://localhost:5500/phishguard_v2.html)***

---
**PhishGuard v2** — *Intelligent Detection. Premium Protection.*
