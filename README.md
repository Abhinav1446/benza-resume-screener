# Benza Resume Screener 🎯

An intelligent AI-powered resume screening system built with **n8n**, **Google Gemini AI**, **Gmail**, and **Google Sheets** that automatically evaluates candidates, scores their resumes against a job description, makes selection decisions, and sends personalised emails — all triggered from a **Google Form submission**.

> This is **Version 1** of a 3-version project. Version 2 adds PDF upload support. Version 3 adds personalised improvement suggestions for rejected candidates.

---

## 🚀 The Problem It Solves

In cities like Hyderabad, a single software engineer job post can receive **1000+ applications**. HR teams spend days manually reading resumes, scoring candidates, and sending responses. This system automates the entire process — from form submission to email response — in seconds.

---

## ✨ Features

- 📋 **Google Form Input** — Candidates submit via a realistic HR form
- 🧠 **AI Resume Extraction** — Gemini extracts skills, experience, projects and education
- 📊 **Weighted Scoring System** — Scores each candidate across 4 criteria
- 🎯 **Smart Decision Making** — Classifies as Strong, Average or Weak automatically
- 📧 **Personalised Emails** — Selected candidates get a shortlist email, others get a polite rejection
- 📝 **Google Sheets Logging** — Full audit trail with scores and reasons, no duplicate entries

---

## 📊 Scoring Criteria

| Criteria | Weight | Description |
|---|---|---|
| Skills Match | 40 points | How well skills match the job requirements |
| Work Experience | 30 points | Years and relevance of experience |
| Projects | 20 points | Real world projects demonstrating ability |
| Education | 10 points | Degree and educational background |
| **Total** | **100 points** | — |

**Decision Logic:**
- 🟢 **Strong** (80–100) → Shortlisted, receives selection email
- 🟡 **Average** (50–79) → Shortlisted, receives selection email
- 🔴 **Weak** (0–49) → Not selected, receives polite rejection email

---

## 🗺️ Workflow Architecture

```
Google Form Submission
        ↓
Google Sheets Trigger
(fires when new row is added)
        ↓
Gemini Extractor
(extracts name, email, skills, experience, projects, education)
        ↓
Gemini Scorer
(scores resume against job description, returns decision + reason)
        ↓
Code Node — Parse Results
(parses both Gemini outputs into structured data)
        ↓
IF Node — Decision Check
(Strong or Average → True, Weak → False)
        ↓
Selected Email        Rejection Email
(shortlist email)     (polite rejection)
        ↓                    ↓
         Google Sheets Update
         (logs scores, decision, reason)
```

---

## 🔧 Tech Stack

| Tool | Purpose |
|---|---|
| n8n | Workflow automation |
| Google Gemini 2.5 Flash | Resume extraction + scoring |
| Gmail API | Sending selection and rejection emails |
| Google Sheets | Form responses + audit logging |
| Google Forms | Candidate input interface |
| JavaScript | Parsing and structuring Gemini outputs |

---

## 📋 Google Form Fields

The system uses a Google Form with these fields:

- Full Name
- Email Address
- Job Applying For (Python Developer or Data Analyst)
- Your Skills
- Work Experience
- Projects
- Education (Degree)

---

## 🚀 How to Set Up

### Prerequisites

- n8n installed locally or on cloud
- Google Gemini API key
- Gmail account with OAuth2 configured in n8n
- Google Sheets and Google Forms account connected in n8n

### Step 1 — Create Google Form

Create a Google Form with the fields listed above and link it to a Google Sheet (Responses tab → Sheets icon).

### Step 2 — Import Workflow

1. Open n8n
2. Click **"Add Workflow"** → **"Import from File"**
3. Import `Benza_Resume_screener_v1.json`

### Step 3 — Configure Credentials

Update the following in the workflow:

- **Google Sheets Trigger** → connect your Google Sheets account
- **Gemini Extractor and Scorer** → add your Gemini API key
- **Gmail nodes** → connect your Gmail account
- **Google Sheets Update** → connect your Google Sheets account

### Step 4 — Update Sheet URL

In the Google Sheets Trigger and Update nodes, replace the sheet URL with your own Google Sheet URL.

### Step 5 — Customise Job Description

In the **Gemini Scorer** node, update the job description to match your actual hiring requirements.

### Step 6 — Activate

Toggle the workflow ON in n8n. It will now automatically process every new Google Form submission.

---

## 📬 Sample Emails

**Selection Email:**
```
Hi John,

Thank you for applying for the Python Developer position at Benza.

We are pleased to inform you that your profile has been shortlisted 
for the next round of our selection process.

Our HR team will be in touch with you shortly regarding the next steps.

Best regards,
Benza HR Team
```

**Rejection Email:**
```
Hi Jane,

Thank you for applying for the Python Developer position at Benza.

After carefully reviewing your profile, we regret to inform you that 
we will not be moving forward with your application at this time.

We appreciate your interest in Benza and encourage you to apply again 
in the future.

Best regards,
Benza HR Team
```

---

## 🔮 Upcoming Versions

- [x] **Version 1** — Google Form input, AI scoring, selection/rejection emails ✅
- [ ] **Version 2** — PDF resume upload support
- [ ] **Version 3** — Personalised improvement suggestions for rejected candidates

---

## 📁 Repository Structure

```
benza-resume-screener/
│
├── Benza_Resume_screener_v1.json    # n8n workflow file
└── README.md                        # This file
```

---

## 👨‍💻 Built By

**Abhinav Gottiparthi**

Built as part of a series of practical AI automation projects.

- GitHub: [@Abhinav1446](https://github.com/Abhinav1446)
- LinkedIn: [Abhinav Gottiparthi](https://www.linkedin.com/in/abhinav-gottiparthi-2022a0237)
