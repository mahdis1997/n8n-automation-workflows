# n8n Automation Workflows

A collection of practical **n8n automation workflows** built to demonstrate real-world automation patterns using APIs, webhooks, conditional logic, custom JavaScript, data processing, notifications, and persistent storage.

The workflows are designed to use **free APIs and services whenever possible**, making them easy to reproduce for learning, portfolio development, and experimentation.

---

## 🚀 Projects

| Workflow                   | Description                                                                    | Main Concepts                                                          |
| -------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------- |
| 📰 `news-digest-bot`       | Collects and processes technology news and sends a digest to Telegram          | RSS, API integration, Code Node, deduplication, scoring, Google Sheets |
| ₿ `crypto-market-watchdog` | Monitors cryptocurrency prices and sends alerts when significant changes occur | Scheduled Trigger, REST API, conditional logic, Telegram               |
| ⭐ `github-tech-radar`      | Discovers interesting GitHub repositories and sends a weekly technology report | GitHub API, data filtering, Code Node, Telegram, Discord Webhook       |
| 💼 `remote-job-tracker`    | Tracks new remote job postings and notifies about new matching jobs            | REST API, keyword filtering, deduplication, Google Sheets, Telegram    |

---

# 📰 1. News Digest Bot

### Overview

`news-digest-bot` automatically collects technology news from multiple RSS feeds, processes and ranks the articles, removes duplicate content, and sends a curated digest to Telegram.

Processed information is also stored in Google Sheets for logging and tracking.

### Sources

* TechCrunch
* Hacker News
* Wired

### Workflow

```text
Schedule Trigger
       ↓
RSS Feed 1 ─┐
RSS Feed 2 ─┼──→ Merge
RSS Feed 3 ─┘
       ↓
Data Processing
       ↓
Remove Duplicates
       ↓
Score Articles
       ↓
Select Top Articles
       ↓
Telegram Notification
       ↓
Google Sheets Log
```

### Key Concepts

* Scheduled automation
* Multiple RSS sources
* Data normalization
* Duplicate detection
* Custom JavaScript with Code Node
* Article scoring
* Telegram Bot API
* Google Sheets integration
* Persistent logging

---

# ₿ 2. Crypto Market Watchdog

### Overview

`crypto-market-watchdog` periodically monitors cryptocurrency prices and detects significant price movements.

The workflow currently monitors:

* Bitcoin (BTC)
* Ethereum (ETH)
* Solana (SOL)

Price data is retrieved from **CoinGecko's public API**, and significant changes trigger a Telegram notification.

### Detection Logic

```text
Every 15 Minutes
       ↓
CoinGecko API
       ↓
BTC / ETH / SOL Prices
       ↓
Compare With Previous Price
       ↓
Change > 3% ?
     ↙       ↘
   YES        NO
    ↓          ↓
Telegram    Continue
 Alert
```

### Key Concepts

* Schedule Trigger
* REST API
* JSON processing
* State comparison
* Conditional branching
* Threshold detection
* Telegram notifications
* Automated monitoring

> **Note:** This workflow is intended for monitoring and automation experiments, not financial advice or trading execution.

---

# ⭐ 3. GitHub Tech Radar

### Overview

`github-tech-radar` searches GitHub for interesting repositories and generates a periodic technology radar.

The workflow can filter repositories based on criteria such as:

* Stars
* Programming language
* Repository activity
* Topics
* Creation/update information

The generated report is delivered through:

* Telegram
* Discord Webhook

### Workflow

```text
Weekly Schedule
       ↓
GitHub API
       ↓
Fetch Repositories
       ↓
Filter / Sort
       ↓
Generate Report
       ↓
    ┌──┴────┐
    ↓       ↓
Telegram  Discord
    ↓       ↓
 Notifications
       ↓
Google Sheets
```

### Key Concepts

* GitHub API integration
* Scheduled automation
* API pagination/data processing
* Filtering and sorting
* Custom Code Node
* Report generation
* Telegram Bot API
* Discord Webhooks
* Google Sheets storage

---

# 💼 4. Remote Job Tracker

### Overview

`remote-job-tracker` periodically checks remote job listings and identifies new opportunities matching predefined keywords.

The workflow uses **RemoteOK** as the job data source.

Matching jobs are compared against previously processed jobs using Google Sheets to prevent duplicate notifications.

### Example Keywords

Keywords can be customized depending on the target role:

```text
Python
Django
FastAPI
Machine Learning
AI
Automation
n8n
Backend
Data
```

### Workflow

```text
Every 6 Hours
       ↓
RemoteOK API
       ↓
Extract Job Listings
       ↓
Keyword Filtering
       ↓
Check Google Sheets
       ↓
Already Seen?
     ↙       ↘
   YES        NO
    ↓          ↓
  Ignore     Notify
                ↓
            Telegram
                ↓
         Save Job to Sheet
```

### Key Concepts

* Scheduled job tracking
* REST API
* Keyword-based filtering
* Data normalization
* Deduplication
* Google Sheets as lightweight storage
* Telegram notifications
* Conditional branching

---

# 🧩 Technologies & Concepts

These workflows demonstrate several important automation and integration patterns:

### Automation

* n8n
* Schedule Trigger
* Conditional branching
* Workflow orchestration

### APIs

* REST APIs
* RSS feeds
* GitHub API
* CoinGecko API
* RemoteOK API

### Programming

* JavaScript
* n8n Code Node
* Data transformation
* Filtering
* Sorting
* Deduplication
* Business logic

### Notifications

* Telegram Bot API
* Discord Webhooks

### Storage

* Google Sheets
* Workflow state
* Historical logs
* Deduplication records

---

# 🔐 Credentials & Security

The workflows are designed to avoid paid API keys whenever possible.

However, some integrations require user-specific credentials.

### Telegram

Create a Telegram bot using **BotFather** and configure the Telegram credential in n8n.

You will need:

```text
Telegram Bot Token
Telegram Chat ID
```

### Google Sheets

Connect your Google account through n8n's Google Sheets credentials.

The workflows use Google Sheets for:

```text
Digest Log
Last Prices
Repo Archive
Seen Jobs
```

### Discord

The GitHub Tech Radar workflow can optionally send reports to Discord through a Webhook.

Store the webhook URL securely and **never commit it to GitHub**.

---

# 📊 Google Sheets Structure

Create the following sheets before running the workflows.

## Digest Log

Example columns:

```text
title
url
source
score
published_at
timestamp
```

## Last Prices

Example columns:

```text
symbol
price
timestamp
```

## Repo Archive

Example columns:

```text
name
url
stars
language
description
timestamp
```

## Seen Jobs

Example columns:

```text
job_id
title
company
url
timestamp
```

The exact column names should match the fields configured inside the corresponding workflow.

---

# ⚙️ Installation

## 1. Install n8n

You can run n8n locally or use a hosted n8n instance.

For a local installation:

```bash
npm install n8n -g
```

Then:

```bash
n8n start
```

---

## 2. Clone the Repository

```bash
git clone https://github.com/mahdis1997/n8n-automation-workflows.git
```

Enter the project directory:

```bash
cd n8n-automation-workflows
```

---

## 3. Import a Workflow

Open n8n and import the desired `.json` workflow.

For example:

```text
news-digest-bot.json
crypto-market-watchdog.json
github-tech-radar.json
remote-job-tracker.json
```

---

## 4. Configure Credentials

Configure the required credentials inside n8n:

```text
Telegram
Google Sheets
```

Discord can be configured through a Webhook for the GitHub Tech Radar workflow.

---

# 🔒 Environment Variables

If environment variables are used, keep sensitive values outside the workflow files.

Example:

```env
TELEGRAM_CHAT_ID=your_chat_id
DISCORD_WEBHOOK_URL=your_webhook_url
```

### Never commit:

```text
.env
API keys
Bot tokens
Passwords
Private webhook URLs
OAuth credentials
```

Make sure sensitive files are included in `.gitignore`.

Example:

```gitignore
.env
*.env
credentials.json
node_modules/
__pycache__/
```

---

# 🏗️ Automation Patterns Demonstrated

These projects intentionally cover common patterns used in real-world automation systems.

### 1. Scheduled Automation

```text
Schedule → Fetch → Process → Notify
```

### 2. Multi-Source Aggregation

```text
Source A ─┐
Source B ─┼→ Merge → Process
Source C ─┘
```

### 3. Conditional Automation

```text
Data
 ↓
Condition
 ├── TRUE  → Action
 └── FALSE → Continue
```

### 4. Custom Business Logic

JavaScript Code Nodes are used when built-in n8n nodes are not sufficient for:

* Scoring
* Filtering
* Deduplication
* Data transformation
* Custom calculations

### 5. Persistent State

Google Sheets is used as lightweight persistent storage for:

* Previously processed items
* Previous cryptocurrency prices
* Job history
* Workflow logs

### 6. Multi-Channel Notifications

The workflows demonstrate sending automated results to different communication channels:

```text
Automation
    ↓
Report
 ┌──┴─────┐
 ↓        ↓
Telegram Discord
```

---

# 📁 Repository Structure

```text
n8n-automation-workflows/
│
├── news-digest-bot/
│   └── news-digest-bot.json
│
├── crypto-market-watchdog/
│   └── crypto-market-watchdog.json
│
├── github-tech-radar/
│   └── github-tech-radar.json
│
├── remote-job-tracker/
│   └── remote-job-tracker.json
│
├── README.md
└── .gitignore
```

---

# 🎯 Purpose

This repository was created as a practical portfolio demonstrating how **n8n can be used to build API-driven automation systems**.

The projects focus on real-world patterns rather than isolated examples:

* API integration
* Workflow orchestration
* Data processing
* Automation scheduling
* Conditional logic
* Custom JavaScript
* Deduplication
* Notifications
* Lightweight data persistence
* Multi-service integration

---

# 🚧 Future Improvements

Possible extensions include:

* AI-powered summarization
* LLM-based job classification
* Semantic search with RAG
* PostgreSQL instead of Google Sheets
* Redis-based state management
* Error handling and retry mechanisms
* Monitoring and logging
* Docker deployment
* Webhook-based triggers
* Automatic workflow health checks
* Dashboard for workflow metrics

---

# 📌 Disclaimer

These workflows are educational and portfolio projects.

External APIs may change their endpoints, rate limits, response formats, or availability. Always check the documentation of the respective service before deploying a workflow in production.

---

## 👩‍💻 Author

**Mahdis**

AI Student | Automation & AI Enthusiast

GitHub: [mahdis1997](https://github.com/mahdis1997)

---

⭐ If you find these workflows useful, feel free to explore, modify, and extend them.

