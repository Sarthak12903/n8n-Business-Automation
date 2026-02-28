# 🤖 AI Business Support Bot — NodeMinds

> An intelligent, always-on AI automation pipeline that obliterates response delays, engages every customer instantly, and scales support operations to infinity — at zero additional cost.

---

## 👥 Team Members

| Name | Role |
|------|------|
| Nitesh Ranjankar | Team Lead & Workflow Architect |
| *(Member 2)* | AI Prompt Engineer |
| *(Member 3)* | Frontend & Form Design |
| *(Member 4)* | Integration & Testing |

> **Team Name:** TriggerX
> **Hackathon:** Pandora Hackathon 2026
> **Theme:** AI + n8n Automation

---

## 🚨 Problem Statement

To address the critical gap in real-time customer engagement for small and medium enterprises by leveraging AI-driven natural language processing and workflow automation to deliver instant, context-aware query resolution — eliminating operational dependency on manual support infrastructure.

---

## 💡 Solution Approach

TriggerX is a **multi-tenant AI customer support platform** where any small business registers their profile once — and instantly gets a 24/7 AI-powered support bot with zero coding required.

When a customer submits a query:

1. **n8n Webhook** receives the form submission instantly
2. **Business Registry Lookup** fetches the specific business's profile from Google Sheets
3. **Sentiment Detector** (Gemini Call 1) analyzes the customer's emotional tone — ANGRY, HAPPY, CONFUSED, FRUSTRATED, or NEUTRAL
4. **AI Reply Generator** (Gemini Call 2) crafts a personalized, sentiment-aware, language-matched reply
5. **Smart Router** escalates complaints/refund queries to human agents
6. **Gmail** delivers the AI reply to the customer within 15 seconds
7. **Google Sheets Logger** records every interaction with full audit trail

```
Customer Query (Tally Form)
        ↓
Webhook → Edit Fields → Business Registry Lookup
                                ↓
                      Sentiment Detector (Gemini #1)
                                ↓
                      AI Reply Generator (Gemini #2)
                                ↓
                           IF Node
                        ↙          ↘
                   ANGRY/          NORMAL
                  COMPLAINT        QUERY
                      ↓               ↓
               Escalate to      Gmail Reply
               Human Agent    + Sheets Logger
```

---

## 🛠️ Tech Stack

| Technology | Purpose | Cost |
|------------|---------|------|
| **n8n** | Workflow automation backbone | Free (self-hosted) |
| **Google Gemini 1.5 Flash** | AI language model (x2 chained calls) | Free tier |
| **Tally.so** | Customer-facing query form | Free |
| **Gmail API** | Automated email delivery | Free |
| **Google Sheets** | Business registry + interaction logging | Free |
| **ngrok** | Public webhook tunnel | Free |
| **Node.js** | Runtime environment for n8n | Free |
| **Fedora Linux** | Operating system | Free |

> 💰 **Total Infrastructure Cost: ₹0**

---

## ⚙️ Installation Steps

### Prerequisites
- Fedora Linux (or any Linux distro)
- Google Account
- Node.js v18+

### 1. Install Node.js
```bash
sudo dnf install nodejs -y
node -v
npm -v
```

### 2. Fix npm Permissions
```bash
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

### 3. Install n8n
```bash
npm install -g n8n
```

### 4. Install ngrok
```bash
npm install -g ngrok
```

### 5. Authenticate ngrok
```bash
ngrok config add-authtoken YOUR_NGROK_TOKEN
```
Get your token at: https://ngrok.com

### 6. Set Up Google Cloud OAuth
- Go to https://console.cloud.google.com
- Create project: `n8n-support-bot`
- Enable **Gmail API** and **Google Sheets API**
- Create OAuth 2.0 credentials (Web Application)
- Add redirect URI: `http://localhost:5678/rest/oauth2-credential/callback`
- Add yourself as Test User in OAuth Consent Screen

### 7. Get Gemini API Key
- Go to https://aistudio.google.com/app/apikey
- Create API Key and copy it

---

## 🚀 How to Run

### Every time you start the bot:

**Terminal 1 — Start n8n:**
```bash
n8n
```

**Terminal 2 — Start ngrok:**
```bash
ngrok http 5678
```

**Then:**
1. Open `http://localhost:5678` in browser
2. Open **"AI Business Support Bot"** workflow
3. Update Tally webhook URL with new ngrok URL:
   ```
   https://xxxx.ngrok-free.app/webhook/support-bot
   ```
4. Toggle **Activate** switch to ON (green)

### Import Workflow
1. Download `workflow.json` from this repo
2. In n8n → click **"Import from file"**
3. Select `workflow.json`
4. Configure credentials (Gemini API, Gmail OAuth, Google Sheets OAuth)
5. Activate workflow

### Test with curl
```bash
curl -X POST http://localhost:5678/webhook/support-bot \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Rahul Sharma",
    "email": "your-email@gmail.com",
    "query": "What are your business hours?",
    "store": "BREW001"
  }'
```

---

## ✨ Features

### Core Features
- **⚡ Instant AI Replies** — Customer gets a response within 15 seconds, 24/7
- **🏢 Multi-Tenant Platform** — Supports unlimited businesses from a single workflow
- **📋 Business Registry** — Add any new business by inserting one row in Google Sheets
- **📧 Automated Email Delivery** — Personalized replies sent directly via Gmail

### AI Features
- **🧠 Dual Gemini AI Calls** — Sentiment detection + reply generation chained together
- **😊 Sentiment Analysis** — Detects ANGRY, FRUSTRATED, HAPPY, CONFUSED, NEUTRAL and adapts tone
- **🌐 Multi-Language Support** — Auto-detects and replies in Hindi, Marathi, Tamil, Telugu, English
- **🎯 Context-Aware Replies** — Each reply is specific to the business's products, policies, and tone

### Smart Routing
- **🚨 Auto Escalation** — Complaints, refund queries, legal issues routed to human agent
- **📬 Dynamic Escalation Email** — Each business has its own escalation contact

### Analytics & Logging
- **📊 Full Audit Trail** — Every interaction logged in Google Sheets with timestamp
- **😤 Sentiment Logging** — Emotion detected for every query stored for analytics
- **📈 Business Intelligence** — Query patterns, response history per business

---

## 🔮 Future Scope

### Short Term
- **WhatsApp Integration** via Twilio API — Reply on WhatsApp instead of just email
- **Follow-up Satisfaction Bot** — Auto-send satisfaction survey 24hrs after reply
- **Slack/Telegram Escalation** — Ping human agent on messaging apps with full context

### Medium Term
- **FAQ Knowledge Base (RAG)** — Store FAQs per business, inject into AI prompt for higher accuracy
- **Voice Query Support** — Customer records voice note → Whisper API transcribes → AI replies
- **Web Dashboard** — Real-time analytics dashboard for businesses to monitor queries

### Long Term
- **SaaS Platform** — Self-serve onboarding portal where businesses register themselves
- **CRM Integration** — Connect with Zoho, HubSpot, Salesforce for customer history context
- **Proactive Outreach** — AI identifies common queries and sends preemptive FAQs to customers
- **Vernacular Voice Bot** — Full IVR system in regional Indian languages for phone support

---

## 📁 Project Structure

```
ai-support-bot/
├── workflow.json          # n8n workflow export (import this into n8n)
├── Business_Registry.xlsx # Business metadata store
├── README.md              # This file
└── docs/
    └── AI_Support_Bot_Documentation.docx  # Full build documentation
```

---

## 📸 Workflow Screenshot

> *(Add your n8n canvas screenshot here)*

```
Webhook → Edit Fields → Get row(s) in sheet → Sentiment Detector → Basic LLM Chain → IF
                                                      |                                ↓
                                               Google Gemini              Gmail + Google Sheets
```

---

## 📜 License

MIT License — Free to use, modify, and distribute.

---

## 🙏 References

- [n8n Documentation](https://docs.n8n.io)
- [Google Gemini API](https://aistudio.google.com)
- [Tally.so Webhooks](https://tally.so/help/webhooks)
- [Gmail API OAuth Guide](https://developers.google.com/gmail/api)
- [ngrok Documentation](https://ngrok.com/docs)
- MSME Ministry India Report 2023 — 63M registered small businesses
- Salesforce State of Service Report 2024 — 83% customers expect instant responses

---

<p align="center">Built with ❤️ by NodeMinds — Pandora Hackathon 2026</p>
