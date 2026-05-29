# NIAT Insider Article Automation

Automatically generates and submits articles to [niatinsider.com](https://www.niatinsider.com/contribute/write) using AI-generated content via the Groq API and browser automation via Playwright.

## What It Does

- Uses **Groq (LLaMA 3.1 8B)** to generate a unique article title, subtitle, and body on the topic of *Career & Wins*
- Uses **Playwright (Firefox)** to open the NIAT Insider submission page and fill in the form
- Submits the article for review automatically
- Repeats every **10.5 minutes** in a loop

## Requirements

- Python 3.12+
- A [Groq API key](https://console.groq.com/keys)

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/anandmahadev/niat_automations.git
cd niat_automations
```

### 2. Install dependencies

```bash
pip install playwright groq python-dotenv
playwright install
```

### 3. Configure your API key

Create a `.env` file in the project root:

```
GROQ_API_KEY=your_groq_api_key_here
```

> ⚠️ Never commit your `.env` file. It is already listed in `.gitignore`.

### 4. Load environment variables & run

```bash
# On Windows (PowerShell)
python niatinsider_automation.py

# On macOS/Linux
python niatinsider_automation.py
```

> The script uses `python-dotenv` to automatically load your `.env` file — no manual exporting needed.

## How It Works

```
Groq API (LLaMA 3.1 8B)
    └── Generate title
    └── Generate subtitle (based on title)
    └── Generate body (3–4 paragraphs)
            │
            ▼
Playwright (Firefox, persistent session)
    └── Navigate to submission page
    └── Select "Career & Wins" category
    └── Fill title, subtitle, body fields
    └── Click "Submit for Review"
            │
            ▼
Wait 10.5 minutes → Repeat
```

## Notes

- The script uses a **persistent Firefox profile** stored at `~/.niat_firefox_profile` so you stay logged in between runs
- The browser runs in **headed mode** (`headless=False`) so you can watch it work
- If an error occurs, it logs the error and continues to the next cycle
