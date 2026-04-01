# 🤖 FoodMate — AI Restaurant Chatbot (n8n)

> A no-code AI chatbot built with n8n that handles customer questions, shares your menu, takes table reservations, and pings you on Telegram — all automatically.

![n8n workflow](https://img.shields.io/badge/n8n-workflow-orange)
![AI chatbot](https://img.shields.io/badge/AI-chatbot-blue)
![beginner friendly](https://img.shields.io/badge/beginner-friendly-green)
![restaurant automation](https://img.shields.io/badge/restaurant-automation-purple)

---

## ✨ What FoodMate Can Do

| Feature | Description |
|---|---|
| 💬 **Answer questions** | Responds to common customer queries about hours, location, and policies |
| 🍽️ **Share the menu** | Fetches live menu data from Google Sheets and answers price, ingredient, and availability queries |
| 📅 **Reserve tables** | Collects guest details conversationally and confirms bookings in real time |
| 📲 **Notify the owner** | Sends reservation summaries and urgent alerts via Telegram (or WhatsApp, etc.) |

---

## 🛠️ Tech Stack

| Tool | Role | Notes |
|---|---|---|
| **n8n** | Workflow automation | Self-hosted or cloud |
| **Gemini / any LLM** | AI chat model | GPT-4, Claude, etc. all work |
| **Redis** | Chat memory | Recommended for speed; Postgres, MongoDB, Xata also work |
| **Google Sheets** | Live menu data | Upload your menu to Google Drive first |
| **Telegram** | Owner notifications | Can be swapped for WhatsApp or any messaging platform |

---

## 🔧 n8n Nodes Used

1. `When Chat Message Received`
2. `AI Agent`
   - Gemini Chat Model *(or any LLM)*
   - Redis Chat Memory *(or Postgres / MongoDB / Xata)*
   - Google Sheets Tool — `Get Row(s)` operation
   - Date & Time Tool
   - Telegram Tool — `Send Message` operation

---

## 🚀 Step-by-Step Build Guide

### Step 1 — Add the trigger node
In n8n, add a **When Chat Message Received** node as your entry point.

### Step 2 — Add an AI Agent node
Connect an **AI Agent** node to the trigger. This is the brain of your chatbot.

### Step 3 — Choose a chat model
Select any model — Gemini, GPT-4, Claude, etc. Gemini works well and has a free tier.

### Step 4 — Set up chat memory
Add **Redis Chat Memory** so the bot remembers previous messages in the same conversation.

### Step 5 — Connect Google Sheets (menu)
Add a **Google Sheets** tool, set the operation to **Get Row(s)**, and link your menu spreadsheet. Upload it to Google Drive first if needed.

> 📌 Need help with Google Sheets credentials? [Check out this guide →](https://github.com/Jawad2011/How-to-get-Google-credential-for-n8n)

### Step 6 — Add Date & Time
Add the **Date & Time** node. In settings, set the timezone using the format `Continent/City`.

```
Example: Asia/Dhaka
```

### Step 7 — Add Telegram notifications
Add a **Telegram Tool**, choose **Send Message**, connect your bot, and paste in your Chat ID.

### Step 8 — Paste the system prompt
Go back to the AI Agent node, open **System Message**, and paste the prompt below.

---

## 🧠 System Prompt

Paste this into **AI Agent → System Message**:

```
## Role
You are a friendly and professional AI assistant for our restaurant.
Your name is "FoodMate". You help customers with menu inquiries,
table reservations, and general questions about the restaurant.

---

## Tools Available

### 1. Get Menu
Use this tool to fetch the current menu from the connected spreadsheet.
- Always call this tool before answering ANY menu-related question.
- Never guess or recall menu items from memory — the spreadsheet is the single source of truth.

### 2. Date & Time Tool
Use this tool to get the current date and time.
- Call before confirming any reservation to verify the date/time is in the future.
- Operating hours: Monday–Friday 12:00–22:00, Saturday–Sunday 11:00–23:00.

### 3. Send Updates Tool
Use this tool for:
a) TABLE RESERVATIONS — send structured update to owner: name, phone, party size, date, time, special requests.
b) OWNER ALERTS — notify for urgent issues (complaints, allergies, accessibility needs).

---

## Reservation Flow
Collect these details conversationally (do not ask all at once):
1. Customer full name
2. Contact phone number
3. Number of guests
4. Preferred date
5. Preferred time
6. Special requests
7. Preferred menu items

Then confirm details → use Date & Time tool → call Send Updates tool → confirm booking to customer.

---

## Rules
- Never guess menu items — always fetch from the sheet
- Never confirm a reservation without all required fields
- Flag food allergies clearly in the owner update
- Keep responses warm, short, and personal (use the customer's name once you know it)
- Do not discuss topics unrelated to the restaurant
```

---

## 💡 Pro Tip

> **Name your nodes descriptively** — e.g. *"Get Menu from Sheets"*, *"Send Telegram Alert"*.
> The AI Agent uses node names to decide which tool to call. Clearer names = smarter routing.

---

## 📥 Quick Start

You can **download the workflow JSON** and import it directly into n8n to get started instantly without building from scratch.

---

## 🙋 Questions & Support

Got a question? Open a [GitHub Discussion](../../discussions) and I'll help out.

If this project helped you, please give it a ⭐ — it helps others find it!

---

*Built by [Jawad](https://github.com/Jawad2011) · Beginner-level n8n project · Open source*
