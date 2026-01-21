# 📧 Gmail Important Email Alerts to Telegram (n8n)
## 📌 Documentation (Version : 1)
### Project Type
Automation | Notification | Email Monitoring | n8n Workflow

## 🧠 Overview
This project implements an automated email monitoring and alerting system using n8n.  
It continuously monitors a Gmail inbox and sends real-time Telegram alerts when important emails are detected based on predefined keywords.
This workflow is designed to reduce the risk of missing critical communications such as:
Financial aid updates
Internship opportunities
Payment or fee notifications
Urgent requests

## 🎯 Objectives
Automatically monitor incoming Gmail messages
Detect important emails using keyword-based logic
Instantly notify the user via Telegram
Reduce manual email checking
Serve as a foundation for AI-based classification (future versions)

## 🧩 System Architecture
Gmail Inbox → Gmail Trigger (n8n) → Text Normalization → KeyWords Filter (If logic) → Message Formatter → Telegram Notification


## ⚙️ Technologies Used


| Component                 | Technology                  |
| ---------------------     | ----------------------------|
| Automation Engine         | n8n                         |
| Email Service             | Gmail (Gmail API)           |
| Messaging Platform        | Telegram Bot API            |
| Logic                     | Keyword-based filtering     |
| Hosting                   | Local / Docker / Cloud      | 


## 🔐 Prerequisites
Before using this workflow, you must have:
* A Gmail account
* An n8n instance (local, Docker, or cloud)
* A Telegram account
* A Telegram bot (created via BotFather)
* Google Cloud project with Gmail API enabled

## 🔑 Keyword Detection Logic
The workflow flags emails as important if the subject or body contains any of the following keywords (case-insensitive):
- financial aid
- internship
- urgent
- payment
- invoice
- fee
- scholarship
These keywords can be easily extended or modified.

# 🛠 Workflow Nodes (Detailed)
## 1️⃣ Gmail Trigger Node
### Purpose:
Listens for new incoming Gmail messages.
Configuration:
Trigger Event: Message Received
Polling Interval: configurable (e.g., every 1–5 minutes)
Data Retrieved:
Sender
Subject
Email snippet/body

## 2️⃣ Set Node – Text Normalization
### Purpose:
Prepares email content for reliable keyword matching.
Logic:
Combines subject and body
Converts text to lowercase
Output Field:
email_text


## 3️⃣ IF Node – Keyword Filter
### Purpose:
Determines whether an email is important.
Logic:
Checks if email_text contains any predefined keyword
Uses OR conditions
Outcome:
TRUE → Continue workflow
FALSE → Stop workflow (no alert)

## 4️⃣ Set Node – Message Formatter
### Purpose:
Creates a readable alert message for Telegram.  
Message Format:  
🚨 Important Email Alert  
  
📩 From: <sender>  
📝 Subject: <subject>  
  
📌 Preview:  
<email snippet>  

🔔 Sent automatically via n8n  


## 5️⃣ Telegram Node – Send Message
### Purpose:
Delivers the alert to a Telegram user or group.
Configuration:
Bot Token (stored securely in n8n credentials)
Chat ID (user or group)
Message content from formatter node

## 🔐 Credentials Setup
Gmail
OAuth 2.0 authentication
Gmail API enabled
Read-only access recommended
Telegram
Bot created using @BotFather
Bot token stored in n8n credentials
Chat ID obtained via Telegram tools

## 🧪 Testing Procedure
1. Send a test email to the monitored Gmail inbox
2. Include a keyword such as “Urgent Payment Notice”
3. Verify:
- Gmail trigger activates
- Keyword filter passes
4. Telegram alert is received

## 🛡 Security Considerations
* Gmail access limited to necessary scopes
* API tokens stored securely in n8n credentials
* No email content stored outside workflow execution
* Alert spam reduced via keyword filtering

## 🚀 Limitations (Version 1)
* Relies on static keywords
* May miss context-based importance
* Cannot classify priority levels
* No AI-based understanding
* These limitations are addressed in future versions.

## 🔄 Planned Enhancements
Version 2: AI-based importance detection (LLM)  
Version 3: Multi-channel alerts (WhatsApp, Messenger)  
Version 4: Risk scoring & SOC dashboard  
Version 5: Multi-user routing & audit logs  
 
