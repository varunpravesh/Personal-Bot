# Personal Expense & Reminder Bot
A set of **n8n workflows** that work together as your **personal finance & reminders assistant**.  
This bot listens to your commands, tracks your expenses, and helps you remember important events — all powered by **Google Sheets** and **AI**.

---

## What This Bot Can Do
- **Log Expenses** – Just tell it `"Biriyani 250"` and it will:
  - Detect the amount
  - Classify it into a category (Food, Groceries, etc.)
  - Save it in the correct Google Sheet tab for the current month
- **Analyze Spending** – Ask:
  - "How much did I spend on food this month?"
  - "Show all grocery expenses last week."
- **Set Reminders** – Use natural language like:
  - "Remind me to pay the electricity bill on 10th at 6 PM"
  - "Schedule a dentist appointment tomorrow at 11 AM"
- **Create Monthly Sheets Automatically**
- **Check Upcoming Events** – "What do I have planned for this weekend?"

---

## Workflows

### 1. **Expense_Tracker**  
The **main controller** workflow that routes your commands to the right place — either logging an expense or triggering a reminder.

---

### 2. **Data_Entry** ([`Data_Entry.json`](Data_Entry.json))  
- Parses messages into expense details (date, item, category, amount).
- Checks if the monthly sheet exists — if not, calls `createSpreadsheet`.
- Appends the entry to Google Sheets.

---

### 3. **createSpreadsheet** ([`createSpreadsheet.json`](createSpreadsheet.json))  
- Creates a **new sheet tab** for the month with headers:
  - `Date`, `Product`, `Category`, `Sub-category`, `Amount`.

---

### 4. **Data_Analysis** ([`Data_Analysis.json`](Data_Analysis.json))  
- AI-powered spending query handler.
- Reads data from your expense sheets.
- Supports natural language questions about your spending habits.

---

### 5. **calendarAgent** ([`calendarAgent.json`](calendarAgent.json))  
- Handles **reminders and events** using Google Calendar.
- Supports creating, updating, deleting, and listing events in **IST**.
- Understands flexible date/time formats ("next Monday at 5", "tomorrow at 10").

---

## Tech Stack
- [n8n](https://n8n.io/) – Automation engine
- Google Sheets API – Expense storage
- Google Calendar API – Event & reminder management
- Azure OpenAI / OpenAI – AI categorization & analysis
- Google Gemini (PaLM) – Alternative AI model

---

## Setup Guide

1. **Import Workflows**  
   In n8n, go to **Import Workflow** and select all `.json` files.

2. **Set Up Credentials**  
   - **Google Sheets OAuth2 API** – For storing expenses
   - **Google Calendar OAuth2 API** – For reminders/events
   - **OpenAI / Azure OpenAI** – For AI categorization
   - **Google Gemini (PaLM)** – Optional AI fallback

3. **Prepare Google Sheets**  
   - Create a spreadsheet named `ExpenseTracking`
   - Make sure your Google Sheets account has edit access

4. **Run the Bot**  
   - Send it messages via your preferred trigger (Telegram, webhook, etc.)
   - Use short commands for expenses, natural language for reminders

---

## 💬 Example Interactions

- You : Ice Cream 500
- Bot : Got it! You spent 500 on Ice cream today (Category: Food, Sub-category: Snack). Shall I save this? 🍦
- You : Yes
- Bot : Yum! That's been saved. Anything else I can track for you? 😊
