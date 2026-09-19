 n8n workflow to automate customer support using Google Gemini (or Groq) and Telegram.

## Features
- **Telegram Trigger:** Listens for customer messages.
- **AI Classification:** Uses Gemini 1.5 Flash to categorize messages.
- **Smart Routing:**
  - **Simple:** Auto-replies using a Google Sheets FAQ.
  - **Complex:** Creates a ticket in Google Sheets and alerts the support team.
- **Logging:** Saves all interactions to Google Sheets.

## Setup
1. **Import:** Upload `ai-support-automation.json` into n8n.
2. **Credentials:** Configure Telegram, Google Gemini API, and Google Sheets.
3. **Config:** Update `YOUR_SUPPORT_TEAM_GROUP_ID` and select your Google Sheet.

## License
MIT
