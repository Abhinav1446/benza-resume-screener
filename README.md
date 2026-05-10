# Benza Resume Screener 🎯

An intelligent AI-powered resume screening system built with **n8n** and **Google Gemini AI** that automatically evaluates candidates, scores resumes against job descriptions, makes selection decisions, and sends personalised emails — including improvement suggestions for rejected candidates.

---

## 🔢 Version History

| Version | Input Method | Key Feature | Status |
|---|---|---|---|
| v1 | Google Form | Text-based screening | ✅ Complete |
| v2 | PDF Upload via Webhook | Automatic PDF extraction | ✅ Complete |
| v3 | PDF Upload via Webhook | Personalised improvement suggestions for rejected candidates | ✅ Complete |

---

## 🚀 The Problem It Solves

In cities like Hyderabad, a single software engineer job post can receive **1000+ applications**. HR teams spend days manually reading resumes, scoring candidates, and sending responses. This system automates the entire process — from resume submission to personalised email response — in seconds.

**Version 3 goes further** — rejected candidates receive a detailed, personalised email explaining exactly why they weren't selected and what specific skills they need to improve to succeed in future applications.

---

## ✨ Features (Version 3 — Latest)

- 📄 **PDF Resume Upload** — Accepts real PDF resumes via POST request
- 🔍 **Automatic PDF Extraction** — Extracts text from PDF natively
- 🧠 **AI Resume Parsing** — Gemini AI extracts skills, experience, projects and education
- 📊 **Weighted Scoring System** — Scores each candidate across 4 criteria
- 🎯 **Smart Decision Making** — Classifies as Strong, Average or Weak automatically
- 📧 **Personalised Selection Email** — Shortlisted candidates receive a professional invitation
- 💡 **Improvement Suggestions** — Rejected candidates receive a warm, detailed email explaining why they weren't selected and exactly what to improve
- 📝 **Google Sheets Logging** — Full audit trail with scores, decisions and reasons
- 🔧 **Single Responsibility Nodes** — Each node does one job for easy debugging

---

## 🗺️ Workflow Architecture (Version 3)

```
POST Request (PDF file + name + email as query params)
        ↓
Webhook Node
        ↓
Extract from File Node
(extracts raw text from PDF)
        ↓
Gemini PDF Extractor
(parses skills, experience, projects, education)
        ↓
Parse Extractor (Code Node)
        ↓
Gemini Scorer
(scores resume against job description)
        ↓
Parse Scorer (Code Node)
        ↓
IF Node — Decision Check
        ↓
Strong/Average (True)          Weak (False)
        ↓                           ↓
Selection Email            Gemini Suggestions ← NEW in v3
                           (generates personalised
                            improvement advice)
                                    ↓
                           Rejection Email
                           (includes suggestions)
        ↓                           ↓
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
- 🟢 **Strong** (80–100) → Shortlisted, receives selection email
- 🟡 **Average** (50–79) → Shortlisted, receives selection email
- 🔴 **Weak** (0–49) → Not selected, receives personalised improvement suggestions

---

## 💡 Sample Rejection Email (Version 3)

```
Hi Ravi,

Thank you for your interest in the Python Developer position at Benza.

After reviewing your application, we were unable to move forward at this time. 
Your current profile scored 12/100 against our requirements. Here's a breakdown:

Skills Gap: Our role requires Python, SQL, and Machine Learning. Your current 
skills in MS Office and basic computer knowledge are a great foundation, but 
you'll need to build technical programming expertise.

How to improve:
- Python: Start with free courses on Coursera or freeCodeCamp (2-3 months)
- SQL: Practice on SQLZoo or HackerRank SQL challenges
- Projects: Build 1-2 real world projects and upload them to GitHub
- Education: Consider certifications in Computer Science fundamentals

We genuinely believe you can bridge this gap. Please don't hesitate to 
apply again once you've built these skills.

Best regards,
Benza HR Team
```

---

## 🔧 Tech Stack

| Tool | Purpose |
|---|---|
| n8n | Workflow automation |
| Gemini 2.5 Flash Lite | Resume text extraction |
| Gemini Flash | Resume scoring + improvement suggestions |
| n8n Extract from File | PDF text extraction |
| Gmail API | Sending selection and rejection emails |
| Google Sheets | Audit logging |
| JavaScript | Parsing Gemini outputs |

---

## 🚀 How to Set Up (Version 3)

### Prerequisites
- n8n installed locally or on cloud
- Google Gemini API key
- Gmail OAuth2 configured in n8n
- Google Sheets OAuth2 configured in n8n

### Step 1 — Import Workflow
1. Open n8n
2. Click **"Add Workflow"** → **"Import from File"**
3. Import `Benza_v3.json` for the latest version

### Step 2 — Configure Credentials
- **Gemini nodes** → add your Gemini API key
- **Gmail nodes** → connect your Gmail account
- **Google Sheets node** → connect your Google account

### Step 3 — Update Sheet URL
In the Google Sheets node, replace the sheet URL with your own Google Sheet URL.

### Step 4 — Customise Job Requirements
In the **Gemini Scorer** and **Gemini Suggestions** nodes, update:
- Job description requirements
- Required skills list
- Minimum experience

### Step 5 — Activate
Toggle the workflow ON in n8n.

---

## 📬 How to Send a Resume

Use **Postman** or any HTTP client:

**URL:**
```
http://localhost:5678/webhook/pdf2?name=John Doe&email=john@example.com
```

**Body:** form-data
| Key | Type | Value |
|---|---|---|
| data | File | candidate_resume.pdf |

---

## ⚠️ Known Limitations

- Free Gemini API has token limits that can affect extraction accuracy for long resumes
- Thinking budget must be set to 0 to prevent token overflow
- Scanned image PDFs are not supported — only text-based PDFs work
- For production use, **Gemini 1.5 Pro** or **Google Document AI** is recommended

---

## 📁 Repository Structure

```
benza-resume-screener/
│
├── Benza_Resume_screener_v1.json    # Version 1 — Google Form input
├── Benza_v2.json                    # Version 2 — PDF upload
├── Benza_v3.json                    # Version 3 — Improvement suggestions
└── README.md                        # This file
```

---

## 👨‍💻 Built By

**Abhinav Gottiparthi**

- GitHub: [@Abhinav1446](https://github.com/Abhinav1446)
- LinkedIn: [Abhinav Gottiparthi](https://www.linkedin.com/in/abhinav-gottiparthi-2022a0237)
