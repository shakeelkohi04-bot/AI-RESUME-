# 📄 ATS Resume Checker

A Streamlit app that analyzes a resume and returns an estimated **ATS score** with specific, prioritized improvements. AI analysis is powered by [Groq](https://groq.com).

## Features

- Upload a resume as **PDF, DOCX or TXT**
- **Overall ATS score (0-100)**, blended from:
  - **Format & structure (40%)**: rule-based checks for contact details, standard section headings, length, bullet points and quantified achievements
  - **Content quality (60%)**: AI review of keywords, impact and clarity
- Optional **job description** input for a tailored **job-match score**
- Prioritized improvements (High / Medium / Low), missing keywords and before/after bullet rewrites
- "Extracted text" view showing what an ATS actually reads from your file
- Download the report as Markdown

> **Note:** No universal "ATS score" exists, because every ATS works differently. Treat the result as a practical estimate, not a guarantee.

## Project structure

```
.
├── app.py             # Streamlit app
├── requirements.txt   # Python dependencies
└── README.md
```

## Run locally

1. **Get a free Groq API key** at <https://console.groq.com/keys>.
2. **Clone and install**
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   python -m venv venv
   source venv/bin/activate        # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. **Provide your API key** (any one of these):
   - Paste it into the app sidebar, or
   - Set an environment variable: `export GROQ_API_KEY="gsk_..."` (Windows PowerShell: `$env:GROQ_API_KEY="gsk_..."`), or
   - Create `.streamlit/secrets.toml`:
     ```toml
     GROQ_API_KEY = "gsk_..."
     ```
4. **Start the app**
   ```bash
   streamlit run app.py
   ```

## Deploy on Streamlit Community Cloud

1. Push this repo to GitHub (keep `.streamlit/secrets.toml` out of it).
2. Go to <https://share.streamlit.io> and sign in with GitHub.
3. Click **Create app** → choose your repo, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and add:
   ```toml
   GROQ_API_KEY = "gsk_your_key_here"
   ```
5. Click **Deploy**.

## Models

The sidebar offers `llama-3.3-70b-versatile` (default), `llama-3.1-8b-instant` and `openai/gpt-oss-120b`, plus a **Custom** option for any other Groq model ID. Groq's catalog changes over time, so check <https://console.groq.com/docs/models> for the current list.

## Limitations

- **Scanned / image-only PDFs** have no extractable text. An ATS can't read them either, so the app asks for a text-based PDF or DOCX.
- Very long resumes are truncated (first ~9,000 characters) to stay within Groq's free-tier limits.
- Multi-column layouts, text boxes and tables can scramble reading order. Check the "Extracted text" tab.
- AI feedback can be imperfect: only add suggested keywords that are true for you.

## Privacy

Resume text is sent to Groq's API for analysis. The app does not store files or text on disk. Results exist only in your browser session.

## Tech stack

Streamlit · Groq API · pypdf · python-docx
