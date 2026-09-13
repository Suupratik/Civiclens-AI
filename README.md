# 🏛️ CivicLens AI

> **Understand. Prioritize. Act.**  
> *Transforming unstructured civic complaints into categorized, explainable priority assessments and ready-to-use reports.*

---

## 💡 Overview

**CivicLens AI** is an AI-powered decision-support system built for civic authorities and proactive citizens. Municipal grievance portals are often overwhelmed with unstructured, emotional complaints. Critical emergencies (like open manholes near schools) frequently get buried beneath routine maintenance requests.

CivicLens AI solves this bottleneck with a **dual-layer architecture**:
1. **Natural Language Understanding (Groq + Llama 3.3)** extracts objective, structured indicators from messy complaint text.
2. **Deterministic Python Priority Engine** transparently computes an auditable urgency score (0–100) based on civil risk formulas.

---

## 🎯 Key Features

- 📝 **Natural Language Ingestion**: Citizens describe issues naturally without navigating bureaucratic dropdowns.
- 📸 **Photo Evidence Attachment**: Upload image evidence verifying infrastructural failure on the grievance dossier.
- 🤖 **AI Classification**: Categorizes complaints into *Road Damage, Garbage & Sanitation, Streetlight, Water & Drainage, Traffic, Public Safety, or Other*.
- 🔎 **Structured Information Extraction**: Extracts duration, location, affected population, hazard level, and documented accident history.
- 🚨 **Deterministic Priority Engine (0–100)**: Transparent, rule-based formula weighting Safety (30%), People (25%), Duration (20%), Frequency (15%), and Public Impact (10%).
- 🎛️ **Interactive What-If Priority Simulator**: Live Plotly radial gauge letting judges slide risk factors and observe real-time score and tier recalculation.
- 🧠 **Explainable AI ("Why this priority?")**: Plain-English bullet points showing exactly why an issue received a `CRITICAL` or `HIGH` rating.
- ⏱️ **Automated Municipal SLA & Escalation Matrix**: Assigns 24h, 48h, 7d, or 14d mandatory action deadlines mapped to designated executive ranks.
- ✍️ **Bilingual Formal Complaint Generator**: Generates formal grievance letters in both **English** and **हिन्दी (Hindi)** with 1-click clipboard copy and `.txt` export.
- 🗺️ **Geospatial Hotspot Map**: Real-time city map charting active civic emergencies across urban wards.
- 📊 **Real-Time Visual Dashboard**: Interactive Plotly metrics and charts tracking categories, priority distribution, and high-risk hotspots.
- 🕘 **In-Memory Session History**: Full session audit log with CSV export capability and zero external database overhead.
- 🛡️ **Zero API Key Dependency**: Runs seamlessly offline with zero latency, zero cost, and 100% pitch stability.

---

## 🏗️ Architecture & Philosophy

```text
              CITIZEN / USER
                    │
                    ▼
          Natural Language Text
                    │
                    ▼
           GROQ API (Llama 3.3)
                    │
                    ▼
      Structured JSON Information Extraction
     (Category, Safety, People, Duration, Incidents)
                    │
                    ▼
      DETERMINISTIC PYTHON PRIORITY ENGINE
                    │
                    ▼
     Explainability ("Why this priority?")
                    │
        ┌───────────┴───────────┐
        ▼                       ▼
 Structured Report       Formal Complaint Letter
        │                       │
        └───────────┬───────────┘
                    ▼
          STREAMLIT APPLICATION
    (Analysis View • Dashboard • History)
```

### 🧠 The Core Differentiator
Many AI applications ask the LLM to simply invent a priority number. This leads to hallucinated scores and unpredictable decisions that municipal bodies cannot legally defend.

**In CivicLens AI:**
> *"The LLM interprets the user's natural language into structured parameters, while our transparent Python-based priority engine calculates the final score deterministically."*

---

## 🧮 Priority Scoring Rubric

$$\text{Priority Score} = (0.30 \times \text{Safety}) + (0.25 \times \text{People}) + (0.20 \times \text{Duration}) + (0.15 \times \text{Frequency}) + (0.10 \times \text{Impact}) + \text{Bonus}_{\text{incident}}$$

| Priority Band | Urgency Level | Required Action SLA |
| :---: | :---: | :--- |
| **76 – 100** | 🔴 **CRITICAL** | Emergency intervention within 24 hours |
| **51 – 75** | 🟠 **HIGH** | Priority dispatch within 48–72 hours |
| **26 – 50** | 🟡 **MODERATE** | Standard scheduled maintenance cycle |
| **0 – 25** | 🟢 **LOW** | Routine civic upkeep |

---

## 🛠️ Tech Stack

- **Core**: Python 3.12, Streamlit
- **LLM / Inference**: Groq API (`llama-3.3-70b-versatile`)
- **Data & Charts**: Pandas, Plotly
- **State Management**: Streamlit `st.session_state` (No SQLite, No Docker, No external DB required)

---

## 🚀 Quickstart Guide

### 1. Clone & Setup Virtual Environment
```bash
git clone https://github.com/your-repo/CivicLens-AI.git
cd CivicLens-AI

python -m venv .venv
# On Windows:
.venv\Scripts\activate
# On Linux/macOS:
source .venv/bin/activate
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. (Optional) Configure Groq API Key
Create a `.env` file from `.env.example`:
```bash
cp .env.example .env
```
Add your free Groq API key:
```env
GROQ_API_KEY=gsk_your_groq_api_key_here
```
*(Note: If no key is set, CivicLens AI automatically operates in resilient offline demo mode).*

### 4. Launch Application
```bash
streamlit run app.py
```
Open your browser at `http://localhost:8501`.

---

## 📁 Repository Structure

```text
CivicLens-AI/
│
├── app.py              # Single monolithic Streamlit application with all modules
├── requirements.txt    # Lean dependencies (Streamlit, Groq, Pandas, Plotly, Dotenv)
├── README.md           # Project pitch, architecture, and instructions
├── .env.example        # Environment variable template
└── .gitignore          # Protected files (.env, .venv, etc.)
```

---

## 🏆 Avalon OpenHack Pitch Defense

1. **Why not a complex multi-service architecture?**  
   For civic triage, simplicity is reliability. Storing session state in memory and deploying a single lightweight Streamlit service eliminates database failovers, cold starts, and complex orchestrations during rapid emergency response.
2. **How does this prevent bias or hallucination?**  
   By strictly separating qualitative interpretation (LLM) from numerical prioritization (Python rules). The rules are open, adjustable by municipal authorities, and 100% auditable.
3. **What is the real-world value?**  
   Turning noisy, emotionally charged complaints into legally sound, formatted grievance letters and clear triage dashboards saves hours of manual dispatcher review per ticket.

---
*Built with ❤️ for Avalon OpenHack.*
