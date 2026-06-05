# 🕷️ Legal Documents Web Scraper —Pakistan High Court (SHC)

> A production-grade Selenium scraper that auto-downloads and classifies 60,000+ Pakistani court judgments from the Sindh High Court and lahore high court etc case law database — because the dataset didn't exist, so I built it.

---

## 🚀 Overview

This project is the **data collection backbone** of my MPhil thesis on Intelligent Legal Research. Pakistani court judgments from SHC (caselaw.shc.gov.pk) were not available as a structured dataset. I engineered a custom pipeline using Selenium WebDriver that:

- Navigates a JS-rendered legal database
- Downloads PDFs automatically via browser automation
- Extracts text from each PDF using `pdfplumber`
- Classifies each judgment into legal category folders
- Names files with citation, year, topic, and court info

**All code in this project was engineered using AI as a thinking partner** — problem defined by me, architecture designed by me, debugged and validated by me. No tutorials were followed.

---

## 📊 Dataset Output

| Metric | Value |
|---|---|
| Total Documents Collected | 60,000+ |
| Source | Sindh High Court — caselaw.shc.gov.pk |
| Document Type | Court Judgments / Case Law PDFs |
| Format | Classified PDFs in category folders |
| Filename Format | `{category}_{topic}_{court}_{year}_{citation}.pdf` |

---

## 📂 Auto-Generated Folder Structure

After running the scraper, PDFs are automatically sorted into:

```
pdfs/
├── civil/          # Civil disputes, contracts, elections, general
├── criminal/       # Section 302, murder, PPC cases
├── bail/           # Bail applications
├── contempt/       # Contempt of court
├── service/        # Government servant / service tribunal
└── tax/            # Income tax, sales tax, customs, FBR
```

**Example filename:**
```
criminal_appeal_shc_2021_CrA1234.pdf
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Selenium WebDriver | Browser automation — JS page rendering, button clicks, pagination |
| webdriver-manager | Auto ChromeDriver installation |
| pdfplumber | PDF text extraction for classification |
| re (regex) | Citation extraction, year detection, text parsing |
| shutil / os | File management, folder creation, duplicate prevention |

---

## 🧠 Classification Logic

After downloading each PDF, the first page text is extracted and classified by keyword matching:

```python
"section 302" / "murder" / "p.p.c"  →  criminal/
"bail"                               →  bail/
"service tribunal"                   →  service/
"income tax" / "fbr"                 →  tax/
"contempt of court"                  →  contempt/
default                              →  civil/
```

Topic sub-tags (`contract`, `election`, `appeal`, `general`) and year are also extracted via regex and embedded in the filename.

---

## 🔄 Pipeline Architecture

```
SHC Case Law Database (JS-rendered)
        ↓
Selenium WebDriver — browser launched with custom download prefs
        ↓
Manual filter applied → ENTER to start scraping
        ↓
Table rows iterated — each row has a download button (td[16])
        ↓
Button clicked via JavaScript executor (no new tab)
        ↓
wait_download() — polls folder until new PDF appears
        ↓
pdfplumber — extracts first page text
        ↓
classify() + topic() + year() + extract_citation_from_row()
        ↓
save_file() — moves PDF to correct folder with smart filename
        ↓
Pagination — "Next" button auto-clicked until no more pages
```

---

## 💡 Key Engineering Decisions

| Problem | Solution |
|---|---|
| JS-rendered pages | Selenium simulates real browser — standard requests fail here |
| PDF opens in browser instead of downloading | `plugins.always_open_pdf_externally: True` in Chrome options |
| New tab hijacking download flow | `execute_script` click — no tab switch needed |
| Duplicate filenames at scale | Loop appends `_1`, `_2` suffix until unique path found |
| Unreliable download timing | `wait_download()` polls directory diff every 1 second up to 15s |
| No structured citation in PDF | Extracted from table row cells (td[1], td[2], td[3]) via fallback loop |

---

## ⚙️ Setup & Run

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/legal-web-scraper.git
cd legal-web-scraper

# Install dependencies
pip install selenium webdriver-manager pdfplumber

# Run scraper
python scraper.py

# In browser: apply your search filters on SHC website
# Then press ENTER in terminal to start downloading
```

> ⚠️ ChromeDriver is auto-managed via `webdriver-manager` — no manual installation needed.

---

## 📁 Project Structure

```
legal-web-scraper/
│
├── scraper.py          # Full pipeline: scrape + classify + save
├── pdfs/
│   ├── civil/
│   ├── criminal/
│   ├── bail/
│   ├── contempt/
│   ├── service/
│   └── tax/
├── downloads_temp/     # Temporary download buffer (auto-cleared)
├── requirements.txt
└── README.md
```

---

## 🔗 Part of a Larger System

This scraper feeds into the **Intelligent Legal Research RAG System** — my MPhil thesis project:

| Phase | Repo |
|---|---|
| 1. Data Collection (SHC Scraper) | ⭐ You are here |
| 2. Metadata Extraction | [legal-metadata-pipeline](#) |
| 3. RAG Pipeline + QA | [legal-research-rag](#) |
| 4. Web Interface | Streamlit (in progress) |

---

## 👩‍💻 Author

**Hafsa** — MPhil Data Science | NLP & AI Engineer | Lahore, Pakistan
🔗 [LinkedIn](https://linkedin.com/in/hafsa904) | 🐙 [GitHub](https://github.com/YOUR_USERNAME)
