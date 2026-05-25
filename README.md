# Job Automation Pipeline

![Status: WIP](https://img.shields.io/badge/status-WIP-orange?style=for-the-badge)

An automated job aggregation, scraping, and AI-powered evaluation pipeline designed to scout entry-level software development roles (AI, Java, Python, Full-Stack, and ML) for freshers (especially MCA graduates) in India.

Built using **n8n**, **Google Gemini**, **Firecrawl**, **Telegram Alerts**, and **Google Sheets**.

> [!NOTE]
> **Status: Work In Progress (WIP) 🚧**
> This pipeline and documentation are currently under active development. Some configurations or integration points may change.

---

## 🚀 Features

- **Multi-Source Aggregation**: Periodically pulls job posts from:
  - **Greenhouse ATS** (Freshworks, Krutrim, Hasura, Razorpay, BrowserStack, Postman, Meesho, Zepto, Groww)
  - **Lever ATS** (Sarvam AI, Yellow.ai, MoEngage, CleverTap, Sprinklr, Chargebee, Zoho)
  - **Remotive** (Global remote developer jobs)
- **Automatic De-duplication**: Integrates with Google Sheets (`SeenJobs` sheet) to record previously processed URLs and skip them on subsequent runs.
- **Deep Scrape (Firecrawl)**: Uses Firecrawl to scrape full Job Descriptions (JD) in markdown format directly from dynamic career pages.
- **AI Decision Maker (Gemini)**: Leverages Gemini to analyze each JD against strict eligibility criteria (e.g., 0-1 years experience, India/Remote, dev-focused) and filter out senior roles, non-dev roles, or unsupported tech stacks.
- **Telegram Alerts**: Sends instantly-formatted Telegram notifications for every qualifying job post.

---

## 🛠️ Tech Stack & Integrations

- **Orchestration**: [n8n](https://n8n.io/)
- **LLM/Decision Engine**: Google Gemini API
- **Web Scraper**: [Firecrawl](https://www.firecrawl.dev/) (Markdown extraction format)
- **Database/Log**: Google Sheets API
- **Notifications**: Telegram Bot API

---

## 📋 Prerequisites & Setup

### 1. Google Sheets Configuration
Create a Google Sheet with two sub-sheets:
- **`CareerPages`**: For storing targets for direct scraping.
  - Columns: `company`, `URL`, `active` (boolean)
- **`SeenJobs`**: For logging evaluated job links.
  - Columns: `job_url`, `job_title`, `company`, `source`, `date_found`

### 2. Required Credentials in n8n
- **Google Sheets OAuth2 API**: For reading targets and logging seen jobs.
- **Google Gemini API (PaLM/Gemini)**: For evaluating the JDs.
- **Telegram Bot API**: Bot token and Chat ID (`8480554995`) for receiving channel alerts.
- **Firecrawl API Key**: Configured via environment variable (`FIRECRAWL_KEY`) or direct headers.

### 3. Workflow Import
1. Clone this repository or copy the contents of [workflow.json](file:///d:/ANTI%20GRAVITY/job-automation-pipeline/workflow.json).
2. Open your **n8n canvas**.
3. Press `Ctrl + F` or go to **Import from File** and upload the `workflow.json` file.
4. Set up the credentials for the nodes, save, and activate!

---

## 📄 License
This project is licensed under the MIT License.
