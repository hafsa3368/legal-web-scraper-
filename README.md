# 🕷️ Legal Documents Web Scraper — 60,000+ Court Judgments

> A production-grade web scraper built to collect Pakistani court judgments from dynamic legal databases — because the dataset didn't exist, so I built it.

---

## 🚀 Overview

This project is the **data collection backbone** of my MPhil thesis on Intelligent Legal Research. Pakistani court judgments were not available as a clean, downloadable dataset. I engineered a custom scraping pipeline using Selenium WebDriver to handle JavaScript-rendered pages and extract 60,000+ legal documents at scale.

**All code in this project was engineered using AI as a thinking partner** — problem defined by me, architecture designed by me, debugged and validated by me. No tutorials were followed.

---

## 📊 Dataset Output

| Metric | Value |
|---|---|
| Total Documents Collected | 60,000+ |
| Source | Pakistani Legal Databases |
| Document Type | Court Judgments / Case Law |
| Format | PDF + Structured Metadata (Excel) |
| Metadata Fields | Case title, court, date, judge, citation, URL |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Selenium WebDriver | Dynamic JavaScript page rendering & navigation |
| Python | Core scripting |
| PyMuPDF | PDF text & metadata extraction |
| OpenPyXL | Structured Excel output for metadata |
| BeautifulSoup | HTML parsing |

---

## 🧠 Why Selenium?

Standard scrapers (requests + BeautifulSoup) fail on legal databases because:
- Pages are **JavaScript-rendered** — content loads dynamically
- Navigation requires **button clicks, dropdowns, pagination**
- Sessions and cookies need to be managed

Selenium WebDriver simulates a real browser — solving all of these problems.

---

## 🔄 Pipeline Architecture

```
Target Legal Database (Dynamic JS pages)
        ↓
Selenium WebDriver — browser automation
        ↓
Page-by-page navigation + pagination handling
        ↓
HTML parsed → document URLs extracted
        ↓
PDFs downloaded at scale
        ↓
PyMuPDF → text + metadata extracted from each PDF
        ↓
OpenPyXL → structured metadata saved to Excel
        ↓
60,000+ documents ready for RAG pipeline
```

---

## 💡 Key Challenges Solved

- **Dynamic rendering:** Selenium handles JS-heavy pages standard scrapers cannot
- **Scale:** Automated pagination to collect thousands of documents without manual intervention
- **Metadata structuring:** Extracted case-level metadata (court, date, judge, citation) from unstructured PDFs using PyMuPDF

---

## ⚙️ Setup & Run

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/legal-web-scraper.git
cd legal-web-scraper

# Install dependencies
pip install -r requirements.txt

# Install ChromeDriver (match your Chrome version)
# https://chromedriver.chromium.org/downloads

# Run scraper
python scraper.py

# Extract metadata
python extract_metadata.py
```

---

## 📁 Project Structure

```
legal-web-scraper/
│
├── scraper.py               # Main Selenium scraping pipeline
├── extract_metadata.py      # PyMuPDF + OpenPyXL metadata extraction
├── config.py                # URLs, pagination settings, file paths
├── requirements.txt
└── README.md
```

---

## 🔗 Part of a Larger System

This scraper feeds into the **Intelligent Legal Research RAG System** — my MPhil thesis project:

| Phase | Repo |
|---|---|
| 1. Data Collection | ⭐ You are here |
| 2. RAG Pipeline + QA | [legal-research-rag](#) |
| 3. Web Interface | [legal-research-streamlit](#) |

---

## 👩‍💻 Author

**Hafsa** — MPhil Data Science | NLP & AI Engineer | Lahore, Pakistan
🔗 [LinkedIn](https://linkedin.com/in/hafsa904) | 🐙 [GitHub](https://github.com/YOUR_USERNAME)
