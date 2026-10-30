# FreshChain 🚛💨

[![License: MIT](https://shields.io)](https://opensource.org)
[![FastAPI](https://shields.io)](https://tiangolo.com)
[![React](https://shields.io)](https://reactjs.org)
[![TailwindCSS](https://shields.io)](https://tailwindcss.com)

**FreshChain** is an intelligent, full-stack cold-chain logistics platform engineered to address supply-chain inefficiencies, freight spoilage, and operational visibility in temperature-sensitive transit networks. By integrating real-time telemetry pipelines with conversational AI systems, the application provides supply-chain managers with end-to-end cargo visibility, rule-based thermal exception handling, and automated risk mitigation workflows.

---

## 🌟 Key Features

- **Real-Time Telemetry Tracking:** Dynamic 3D shipment tracking interfaces utilizing Three.js maps synchronized with mock asset location updates.
- **Dynamic Risk Evaluation Engine:** Algorithmic moving-window temperature trend analysis designed to intercept thermal anomalies and trigger threshold notifications before inventory loss occurs.
- **Conversational Logistics Copilot:** Secure server-side orchestration utilizing the Groq API, enabling operators to analyze fleet statuses through context-aware natural language queries.
- **Asynchronous Exception Logging:** Localized warning mechanisms that monitor vehicle sensor boundaries (e.g., severe climate breaches) and record system trace actions instantly.

---

## 🛠️ Architecture & Tech Stack

- **Frontend:** React.js, Vite, Three.js (pinned to v0.128.0 for precise visual rendering), TailwindCSS
- **Backend:** Python, FastAPI (Asynchronous API gateway)
- **AI Infrastructure:** Llama-3-8b via Groq API cloud instances
- **Data Layer:** Relational SQLite tracking simulated asset metadata, logistics configurations, and audit paths

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v18 or newer)
- Python 3.10+

### 1. Backend Gateway Configuration
Navigate to the backend directory, initialize a secure virtual runtime, and install the package requirements:
```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: .\venv\Scripts\activate
pip install -r requirements.txt
```

Create a local environment file (`.env`) within the backend directory and configure your credentials:
```text
GROQ_API_KEY=your_production_groq_api_key_here
```

Launch the asynchronous server gateway:
```bash
uvicorn main:app --reload
```

### 2. Frontend Application Setup
Navigate to the frontend directory, install web modules, and configure your runtime endpoints:
```bash
cd ../frontend
npm install
```

Create your frontend web environmental configuration file (`.env`):
```text
VITE_CHAT_URL=http://127.0.0
```

Boot the local Vite development server instance:
```bash
npm run dev
```

---

## 🔒 Security & Environment Governance
- All server keys and API tokens are managed via environment isolation profiles (`.env`) and are protected from repository exposure via configuration control rules within `.gitignore`.
