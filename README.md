# ATS Resume Checker

A Streamlit app that scores a resume for ATS (Applicant Tracking System) friendliness and suggests concrete improvements, using Google's Gemini Flash model.

## Features

- Upload a resume as **PDF, DOCX or TXT**
- Optional **job description** to get a role-specific score and keyword match
- ATS score out of 100 with a breakdown (formatting, keywords, experience impact, education, readability)
- Strengths, weaknesses, prioritised improvements, matched and missing keywords
- Download the full report as JSON

## Project structure

```
.
├── app.py             # Streamlit app
├── requirements.txt   # Python dependencies
└── README.md
```

## Run locally

1. Get a free Gemini API key at https://aistudio.google.com/apikey
2. Install and run:

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

export GEMINI_API_KEY="your-key"   # Windows PowerShell: $env:GEMINI_API_KEY="your-key"
streamlit run app.py
```

You can also skip the environment variable and paste the key into the sidebar field.

Alternatively, create `.streamlit/secrets.toml` (never commit it):

```toml
GEMINI_API_KEY = "your-key"
```

## Configuration

| Setting | How | Default |
|---|---|---|
| API key | `GEMINI_API_KEY` env var, Streamlit secret, or sidebar field | none |
| Model | `GEMINI_MODEL` env var or sidebar field | `gemini-2.5-flash` |

## Deploy on Streamlit Community Cloud

1. Push this repo to GitHub.
2. Go to https://share.streamlit.io and sign in with GitHub.
3. Click **Create app**, pick the repo, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and add:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
5. Click **Deploy**.

## Notes and limitations

- Scanned or image-only PDFs have no extractable text; export a text-based PDF or DOCX instead.
- The score is an AI estimate of ATS-friendliness, not the output of a real ATS. Treat it as guidance.
- Resumes are sent to Google's Gemini API for analysis. Do not upload anything you are not comfortable sharing with that service.
- Add `.streamlit/secrets.toml` and any `.env` file to `.gitignore`.
