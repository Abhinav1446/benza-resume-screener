# Benza Resume Screener — Version 2 🎯

An upgraded version of the Benza Resume Screener that accepts **PDF resume uploads via webhook** instead of Google Form text input. Automatically extracts candidate information from PDF files, scores them against a job description, and sends personalised selection or rejection emails.

> This is **Version 2** of a 3-version project.
> - ✅ Version 1 — Google Form text input
> - ✅ Version 2 — PDF upload via webhook (this version)
> - 🔜 Version 3 — Personalised improvement suggestions for rejected candidates

---

## 🆕 What's New in Version 2

| Feature | Version 1 | Version 2 |
|---|---|---|
| Input method | Google Form (text) | PDF upload via webhook |
| Resume parsing | Manual text fields | Automatic PDF extraction |
| Integration | Google Forms trigger | REST API webhook |
| Use case | Internal HR form | Any website or API |

---

## ✨ Features

- 📄 **PDF Resume Upload** — Accepts real PDF resumes via POST request
- 🔍 **Automatic PDF Extraction** — Extracts text from PDF using n8n's Extract from File node
- 🧠 **AI Resume Parsing** — Gemini AI extracts skills, experience, projects and education
- 📊 **Weighted Scoring** — Scores candidate across 4 criteria against job description
- 🎯 **Smart Decision Making** — Classifies as Strong, Average or Weak
- 📧 **Personalised Emails** — Sends appropriate email based on decision
- 📝 **Google Sheets Logging** — Full audit trail with no duplicate entries
- 🔧 **Single Responsibility Nodes** — Each node does one job for easy debugging

---

## 🗺️ Workflow Architecture

```
POST Request (PDF file + name + email as query params)
        ↓
Webhook Node
(receives PDF binary + candidate details)
        ↓
Extract from File Node
(extracts raw text from PDF)
        ↓
Gemini PDF Extractor
(parses skills, experience, projects, education from text)
        ↓
Parse Extractor (Code Node)
(structures Gemini output into clean JSON)
        ↓
Gemini Scorer
(scores resume against job description)
        ↓
Parse Scorer (Code Node)
(combines extracted data + scores into final output)
        ↓
IF Node — Decision Check
(Strong or Average → True, Weak → False)
        ↓
Selected Email        Rejection Email
        ↓                    ↓
         Google Sheets Update
         (logs all data, no duplicates)
```

---

## 📊 Scoring Criteria

| Criteria | Weight | Description |
|---|---|---|
| Skills Match | 40 points | How well skills match job requirements |
| Work Experience | 30 points | Years and relevance of experience |
| Projects | 20 points | Real world projects demonstrating ability |
| Education | 10 points | Degree and educational background |
| **Total** | **100 points** | — |

**Decision Logic:**
- 🟢 **Strong** (80–100) → Shortlisted
- 🟡 **Average** (50–79) → Shortlisted
- 🔴 **Weak** (0–49) → Not selected

---

## 🔧 Tech Stack

| Tool | Purpose |
|---|---|
| n8n | Workflow automation |
| Gemini 2.5 Flash Lite | Resume extraction |
| Gemini Flash | Resume scoring |
| n8n Extract from File | PDF text extraction |
| Gmail API | Sending emails |
| Google Sheets | Audit logging |
| JavaScript | Parsing Gemini outputs |

---

## 🚀 How to Set Up

### Prerequisites

- n8n installed locally or on cloud
- Google Gemini API key
- Gmail OAuth2 configured in n8n
- Google Sheets OAuth2 configured in n8n

### Step 1 — Import Workflow

1. Open n8n
2. Click **"Add Workflow"** → **"Import from File"**
3. Import `Benza_v2.json`

### Step 2 — Configure Credentials

- **Gemini nodes** → add your Gemini API key
- **Gmail nodes** → connect your Gmail account
- **Google Sheets node** → connect your Google account

### Step 3 — Update Sheet URL

In the Google Sheets node, replace the sheet URL with your own Google Sheet URL.

### Step 4 — Customise Job Description

In the **Gemini Scorer** node, update the job description prompt to match your actual hiring requirements.

### Step 5 — Activate

Toggle the workflow ON in n8n.

---

## 📬 How to Send a Resume

Use **Postman** or any HTTP client to send a POST request:

**URL:**
```
http://localhost:5678/webhook/pdf?name=John Doe&email=john@example.com
```

**Body:** form-data
| Key | Type | Value |
|---|---|---|
| data | File | candidate_resume.pdf |

---

## ⚠️ Known Limitations

- Free Gemini API has token limits that can affect extraction accuracy for long resumes
- Thinking budget must be set to 0 to avoid token overflow
- For production use, **Gemini 1.5 Pro** or **Google Document AI** is recommended for more reliable PDF parsing
- Scanned image PDFs are not supported — only text-based PDFs work with the Extract from File node

---

## 📁 Repository Structure

```
benza-resume-screener/
│
├── Benza_Resume_screener_v1.json    # Version 1 — Google Form input
├── Benza_v2.json                    # Version 2 — PDF upload
└── README.md                        # This file
```

---

## 🔮 Upcoming

- [ ] **Version 3** — Personalised improvement suggestions for rejected candidates

---

## 👨‍💻 Built By

**Abhinav Gottiparthi**

- GitHub: [@Abhinav1446](https://github.com/Abhinav1446)
- LinkedIn: [Abhinav Gottiparthi](https://www.linkedin.com/in/abhinav-gottiparthi-2022a0237)
