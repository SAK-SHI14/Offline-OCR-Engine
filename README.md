# 🛡️ VaultOCR: Privacy-First Offline Document Intelligence Engine

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109.0-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![OCR](https://img.shields.io/badge/Engine-Tesseract_5-FF6F00?logo=tesseract&logoColor=white)](https://github.com/tesseract-ocr/tesseract)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

**VaultOCR** is a production-ready, industrial-grade document analysis system designed for environments where **data privacy is non-negotiable**. Unlike cloud-based solutions, VaultOCR processes sensitive documents entirely on local hardware—ensuring no data ever leaves your infrastructure.

---

## ✨ Key Features

-   🔒 **100% Offline Processing**: Zero external API calls. Privacy by design.
-   🏎️ **High-Performance Pipeline**: Multi-layered architecture (Vision → OCR → NLP).
-   📐 **Intelligent Layout Analysis**: Detects tables, headers, and structural blocks using advanced morphological operations.
-   🧪 **Advanced Preprocessing**: Automated deskewing, noise reduction, and adaptive thresholding for poor-quality scans.
-   🛠️ **Enterprise Integration**: Developer-friendly FastAPI endpoints with strict Pydantic validation.
-   📊 **Interactive Dashboard**: Built-in Streamlit UI for real-time processing visualization.

---

## 🏗️ Architecture & Pipeline

The system follows a strict **6-Layer Strategic Pipeline**:

1.  **Ingestion Layer**: Secure validation and memory-safe loading of document images.
2.  **Vision Preprocessing**: Skew correction (rotation), denoising, and contrast enhancement.
3.  **OCR Core**: Multi-pass Tesseract 5 LSTM execution for granular character and coordinate extraction.
4.  **Layout Engine**: Morphological analysis to group text into logical blocks (Headers, Paragraphs, Tables).
5.  **Post-Processing (NLP)**: Regex-driven entity extraction (Dates, Emails, Currency) and text normalization.
6.  **Serialization**: Structured JSON output mapped to strict versioned schemas.

---

## 📂 Project Structure

```text
Offline-OCR-Engine/
└── DocumentEngine/
    ├── app/
    │   ├── api/v1/         # API Endpoints (FastAPI)
    │   ├── core/           # Configuration & Logging
    │   ├── models/         # Pydantic Schemas (Request/Response)
    │   ├── services/       # Core Logic (OCR, Vision, NLP)
    │   │   ├── ingestion.py
    │   │   ├── layout_engine.py
    │   │   ├── ocr_service.py
    │   │   ├── pipeline.py
    │   │   ├── postprocessing.py
    │   │   └── preprocessing.py
    │   └── main.py         # Application Entrypoint
    ├── ui/
    │   └── dashboard.py    # Streamlit Web Interface
    ├── requirements.txt    # Project Dependencies
    └── setup_guide.md      # Detailed Installation Instructions
```

---

## 🚀 Getting Started

### 📦 Prerequisites

1.  **Python 3.10+**
2.  **Tesseract OCR 5.0+**: Ensure the binary is installed locally.
    -   **Windows**: [Download UB Mannheim Installer](https://github.com/UB-Mannheim/tesseract/wiki)
    -   **Linux**: `sudo apt install tesseract-ocr`
    -   **Mac**: `brew install tesseract`

### 🔧 Installation

```bash
# 1. Clone the repository
git clone https://github.com/SAK-SHI14/VaultOCR.git
cd VaultOCR

# 2. Create and activate a virtual environment
python -m venv venv
# Windows:
.\venv\Scripts\Activate.ps1
# Unix:
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt
```

### 🛰️ Running the System

You can run the backend API and the frontend dashboard independently:

#### 1. Start the API Gateway (FastAPI)
```bash
uvicorn app.main:app --reload
```
-   **Documentation**: Visit `http://localhost:8000/docs` for the interactive Swagger UI.

#### 2. Start the Analytics Dashboard (Streamlit)
```bash
streamlit run ui/dashboard.py
```
-   **URL**: Accessible at `http://localhost:8501`.

---

## 🔌 API Documentation

### Process Document
`POST /api/v1/process`

**Request**: `multipart/form-data` containing a `file`.

**Response Excerpt**:
```json
{
  "document_id": "8f2a...",
  "text_content": { "full_text": "Sample text..." },
  "layout": { "blocks": [ ... ] },
  "tables": [ ... ],
  "entities": {
    "dates": ["2024-05-20"],
    "emails": ["info@company.com"]
  },
  "processing_metadata": {
    "runtime_ms": 452.3,
    "ocr_engine": "tesseract"
  }
}
```

---

## �️ Security & Privacy Statement

VaultOCR is built for security-sensitive industries (Finance, Healthcare, Legal). 
- **Zero Cloud Footprint**: Data never touches a third-party server.
- **In-Memory Operations**: Files are processed in RAM and never persisted to disk unless explicitly configured.
- **Audit Ready**: Simple codebase, easy to audit for security compliance.

---

## 🤝 Contributing & License

Contributions are welcome! Please feel free to submit a Pull Request. Distributed under the **MIT License**.

---

*Built with ❤️ for the Open Source Privacy community.*
