# Google Sheets ↔ WhatsApp Automation

Automate WhatsApp messaging using Google Sheets with two-way synchronization powered by **Twilio**, **n8n**, and **Google Sheets**.

---

## 🚀 Overview

This project enables:
- 📤 Sending WhatsApp messages when a new row is added to Google Sheets
- 📥 Receiving WhatsApp replies and storing them back in Google Sheets
- 🔄 Updating message **Status** and **Timestamp** automatically
- 🧩 Scalable, production-ready automation using Twilio (official WhatsApp API)

---

## ✨ Features

- Google Sheets → WhatsApp (auto-send on new row)
- WhatsApp → Google Sheets (store incoming messages)
- Message status tracking (Sent / Failed)
- Timestamp logging
- Phone-number based row matching
- Built using official APIs (no risk of bans)

---

## 🛠 Tech Stack

- **Twilio WhatsApp API**
- **n8n** (workflow automation)
- **Google Sheets**
- **HTTP Request (Twilio API)**
- *(Optional)* Google Apps Script, Slack

---

## 🔄 High-Level Workflow

Google Sheets (New Row)
↓
n8n Trigger
↓
Send WhatsApp Message (Twilio API)
↓
Update Google Sheet (Status + Timestamp)

Incoming WhatsApp Reply
↓
Twilio Webhook
↓
n8n Webhook
↓
Append Reply to Google Sheet

yaml
Copy code
---
## 🖼 Workflow Overview

![n8n Workflow](workflow.png)
---

## 📄 Google Sheet Structure

| Column | Name         | Description                          |
|------|--------------|--------------------------------------|
| A    | Name         | Recipient name                       |
| B    | Phone_Number | WhatsApp number (+CountryCode)       |
| C    | Message      | Message to send                      |
| D    | Status       | Sent / Failed                        |
| E    | Timestamp    | Auto-filled                          |

📌 Phone numbers **must include country code** (example: `+918050823618`)

---

## ⚙️ Setup Instructions

### 1️⃣ Twilio Setup
- Create a Twilio account
- Enable WhatsApp Sandbox (for testing)
- Send `join <sandbox-code>` to `+1 415 523 8886`
- Get **Account SID** and **Auth Token**

---

### 2️⃣ n8n Setup
- Import the workflow JSON
- Add credentials:
  - Google Sheets
  - Twilio (used in HTTP Request Basic Auth)
- Activate the workflow

---

### 3️⃣ WhatsApp Send (HTTP Request)
- Method: `POST`
- URL:
https://api.twilio.com/2010-04-01/Accounts/{ACCOUNT_SID}/Messages.json

yaml
Copy code
- Body (Form URL Encoded):
- From: `whatsapp:+14155238886`
- To: `whatsapp:+91XXXXXXXXXX`
- Body: message text

---

## 📥 Incoming WhatsApp Messages

- Use Twilio **Webhook** → n8n **Webhook Trigger**
- Extract:
- Sender number
- Message body
- Timestamp
- Append to Google Sheet

---

## 💰 Pricing (Important)

- ❌ No lifetime free WhatsApp
- ✅ Twilio is **pay-as-you-go**
- Charged per WhatsApp conversation (Meta pricing applies)
- Suitable for long-term business use

---

## 📌 Notes & Best Practices

- Workflow triggers **only on new rows**, not edits
- Avoid using phone numbers without country code
- Sandbox requires each number to join once
- For production, move to **Twilio WhatsApp Business (paid)**

---

## 👤 Author

**Nithin**  
Automation | Backend | WhatsApp Integrations

---

## 📜 License

MIT License
