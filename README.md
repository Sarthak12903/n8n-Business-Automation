![architecture](https://github.com/user-attachments/assets/149fa7cb-1e1e-4a52-bd56-15d8a74b1b4c)# 🤖 AI Business Support Bot — NodeMinds

> An intelligent, always-on AI automation pipeline that obliterates response delays, engages every customer instantly, and scales support operations to infinity — at zero additional cost.

---

## 👥 Team Members

| Name | 
|------|
| Nitesh Ranjankar | 
| *Ashish Deshmukh* | 
| *Sarthak Bhalerao* |
| *Alina Pathan* |

> **Team Name:** NodeMinds
> **Hackathon:** Pandora Hackathon 2026
> **Theme:** AI + n8n Automation

---

## 🚨 Problem Statement

To address the critical gap in real-time customer engagement for small and medium enterprises by leveraging AI-driven natural language processing and workflow automation to deliver instant, context-aware query resolution — eliminating operational dependency on manual support infrastructure.

---

## 💡 Solution Approach

This is a **multi-tenant AI customer support platform** where any small business registers their profile once — and instantly gets a 24/7 AI-powered support bot with zero coding required.

When a customer submits a query:

1. **n8n Webhook** receives the form submission instantly
2. **Business Registry Lookup** fetches the specific business's profile from Google Sheets
3. **Sentiment Detector** (Gemini Call 1) analyzes the customer's emotional tone — ANGRY, HAPPY, CONFUSED, FRUSTRATED, or NEUTRAL
4. **AI Reply Generator** (Gemini Call 2) crafts a personalized, sentiment-aware, language-matched reply
5. **Smart Router** escalates complaints/refund queries to human agents
6. **Gmail** delivers the AI reply to the customer within 15 seconds
7. **Google Sheets Logger** records every interaction with full audit trail

![architecture](https://github.com/user-attachments/assets/5a1597c5-b51c-42b6-bcf6-38d7fa82c843)<svg width="1200" height="600" xmlns="http://www.w3.org/2000/svg" font-family="Arial, sans-serif">

  <!-- Background -->
  <rect width="1200" height="600" fill="#0f1117" rx="16"/>

  <!-- Title -->
  <text x="600" y="40" text-anchor="middle" fill="#FFFFFF" font-size="18" font-weight="bold">NodeMinds — AI Business Support Bot Architecture</text>
  <text x="600" y="62" text-anchor="middle" fill="#888888" font-size="12">n8n + Google Gemini + Gmail + Twilio + Google Sheets</text>

  <!-- ── ARROW HELPER (reusable lines) ── -->

  <!-- Webhook → Edit Fields -->
  <line x1="138" y1="200" x2="198" y2="200" stroke="#555" stroke-width="2" marker-end="url(#arrow)"/>
  <!-- Edit Fields → Get row(s) -->
  <line x1="308" y1="200" x2="368" y2="200" stroke="#555" stroke-width="2" marker-end="url(#arrow)"/>
  <!-- Get row(s) → Sentiment Detector -->
  <line x1="478" y1="200" x2="538" y2="200" stroke="#555" stroke-width="2" marker-end="url(#arrow)"/>
  <!-- Sentiment Detector → Basic LLM Chain -->
  <line x1="648" y1="200" x2="708" y2="200" stroke="#555" stroke-width="2" marker-end="url(#arrow)"/>
  <!-- Basic LLM Chain → IF -->
  <line x1="818" y1="200" x2="878" y2="200" stroke="#555" stroke-width="2" marker-end="url(#arrow)"/>

  <!-- IF → TRUE path (up to Gmail + Sheets) -->
  <line x1="953" y1="185" x2="1000" y2="185" stroke="#22c55e" stroke-width="2" marker-end="url(#arrowGreen)"/>
  <line x1="1000" y1="185" x2="1000" y2="310" stroke="#22c55e" stroke-width="2"/>
  <line x1="1000" y1="310" x2="1040" y2="310" stroke="#22c55e" stroke-width="2" marker-end="url(#arrowGreen)"/>

  <!-- Gmail → Sheets -->
  <line x1="1110" y1="310" x2="1040" y2="430" stroke="#22c55e" stroke-width="1.5" stroke-dasharray="5,4"/>

  <!-- IF → FALSE path (down to WhatsApp) -->
  <line x1="953" y1="215" x2="1000" y2="215" stroke="#ef4444" stroke-width="2" marker-end="url(#arrowRed)"/>
  <line x1="1000" y1="215" x2="1000" y2="430" stroke="#ef4444" stroke-width="2"/>
  <line x1="1000" y1="430" x2="1040" y2="430" stroke="#ef4444" stroke-width="2" marker-end="url(#arrowRed)"/>

  <!-- Gemini sub-node connector (dashed) to Sentiment Detector -->
  <line x1="693" y1="320" x2="593" y2="255" stroke="#666" stroke-width="1.5" stroke-dasharray="5,4" marker-end="url(#arrowGray)"/>
  <!-- Gemini label -->
  <text x="625" y="310" fill="#888" font-size="10" text-anchor="middle">Model</text>

  <!-- ── ARROWHEAD MARKERS ── -->
  <defs>
    <marker id="arrow" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto">
      <path d="M0,0 L0,6 L8,3 z" fill="#555"/>
    </marker>
    <marker id="arrowGreen" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto">
      <path d="M0,0 L0,6 L8,3 z" fill="#22c55e"/>
    </marker>
    <marker id="arrowRed" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto">
      <path d="M0,0 L0,6 L8,3 z" fill="#ef4444"/>
    </marker>
    <marker id="arrowGray" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto">
      <path d="M0,0 L0,6 L8,3 z" fill="#666"/>
    </marker>
  </defs>

  <!-- ══════════════════════════════════════ -->
  <!--              MAIN NODES               -->
  <!-- ══════════════════════════════════════ -->

  <!-- 1. Webhook -->
  <rect x="48" y="160" width="90" height="80" rx="12" fill="#1e2736" stroke="#3b82f6" stroke-width="2"/>
  <text x="93" y="192" text-anchor="middle" fill="#3b82f6" font-size="22">⚡</text>
  <text x="93" y="212" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Webhook</text>
  <text x="93" y="228" text-anchor="middle" fill="#888" font-size="9">POST /support-bot</text>

  <!-- 2. Edit Fields -->
  <rect x="198" y="160" width="110" height="80" rx="12" fill="#1e2736" stroke="#8b5cf6" stroke-width="2"/>
  <text x="253" y="192" text-anchor="middle" fill="#8b5cf6" font-size="20">✏️</text>
  <text x="253" y="212" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Edit Fields</text>
  <text x="253" y="228" text-anchor="middle" fill="#888" font-size="9">name, email, query, store</text>

  <!-- 3. Get row(s) in sheet -->
  <rect x="368" y="160" width="110" height="80" rx="12" fill="#1e2736" stroke="#22c55e" stroke-width="2"/>
  <text x="423" y="192" text-anchor="middle" fill="#22c55e" font-size="20">📋</text>
  <text x="423" y="210" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Get row(s)</text>
  <text x="423" y="226" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">in sheet</text>
  <text x="423" y="242" text-anchor="middle" fill="#888" font-size="9">Business Registry</text>

  <!-- 4. Sentiment Detector -->
  <rect x="538" y="160" width="110" height="80" rx="12" fill="#1e2736" stroke="#f59e0b" stroke-width="2"/>
  <text x="593" y="192" text-anchor="middle" fill="#f59e0b" font-size="20">🧠</text>
  <text x="593" y="210" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Sentiment</text>
  <text x="593" y="226" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Detector</text>
  <text x="593" y="242" text-anchor="middle" fill="#888" font-size="9">Gemini Call #1</text>

  <!-- 5. Basic LLM Chain -->
  <rect x="708" y="160" width="110" height="80" rx="12" fill="#1e2736" stroke="#f59e0b" stroke-width="2"/>
  <text x="763" y="192" text-anchor="middle" fill="#f59e0b" font-size="20">💬</text>
  <text x="763" y="210" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Basic LLM</text>
  <text x="763" y="226" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Chain</text>
  <text x="763" y="242" text-anchor="middle" fill="#888" font-size="9">Gemini Call #2</text>

  <!-- 6. IF Node -->
  <rect x="878" y="160" width="90" height="80" rx="12" fill="#1e2736" stroke="#64748b" stroke-width="2"/>
  <text x="923" y="192" text-anchor="middle" fill="#64748b" font-size="20">🔀</text>
  <text x="923" y="212" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">IF Node</text>
  <text x="923" y="228" text-anchor="middle" fill="#888" font-size="9">Smart Router</text>

  <!-- TRUE label -->
  <text x="980" y="180" fill="#22c55e" font-size="10" font-weight="bold">TRUE</text>
  <!-- FALSE label -->
  <text x="980" y="225" fill="#ef4444" font-size="10" font-weight="bold">FALSE</text>

  <!-- 7. Gmail (TRUE path) -->
  <rect x="1040" y="270" width="110" height="80" rx="12" fill="#1e2736" stroke="#22c55e" stroke-width="2"/>
  <text x="1095" y="302" text-anchor="middle" fill="#22c55e" font-size="20">📧</text>
  <text x="1095" y="322" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Send a</text>
  <text x="1095" y="338" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Message</text>

  <!-- 8. Append row (TRUE path) -->
  <rect x="1040" y="390" width="110" height="80" rx="12" fill="#1e2736" stroke="#22c55e" stroke-width="1.5" stroke-dasharray="6,3"/>
  <text x="1095" y="422" text-anchor="middle" fill="#22c55e" font-size="20">📊</text>
  <text x="1095" y="440" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">Append Row</text>
  <text x="1095" y="456" text-anchor="middle" fill="#888" font-size="9">in Sheet</text>

  <!-- 9. WhatsApp (FALSE path) -->
  <rect x="1040" y="390" width="110" height="80" rx="12" fill="#1e2736" stroke="#ef4444" stroke-width="2"/>
  <text x="1095" y="422" text-anchor="middle" fill="#ef4444" font-size="20">💬</text>
  <text x="1095" y="440" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">WhatsApp/</text>
  <text x="1095" y="456" text-anchor="middle" fill="#FFFFFF" font-size="11" font-weight="bold">SMS</text>

  <!-- ══════════════════════════════════════ -->
  <!--           GEMINI SUB-NODE             -->
  <!-- ══════════════════════════════════════ -->
  <circle cx="693" cy="340" r="36" fill="#1a1a2e" stroke="#666" stroke-width="1.5" stroke-dasharray="5,3"/>
  <text x="693" y="335" text-anchor="middle" fill="#4285F4" font-size="20">G</text>
  <text x="693" y="352" text-anchor="middle" fill="#888" font-size="9">Gemini Model</text>

  <!-- ══════════════════════════════════════ -->
  <!--         SENTIMENT BADGES              -->
  <!-- ══════════════════════════════════════ -->
  <rect x="48" y="460" width="1110" height="110" rx="10" fill="#0d1117" stroke="#333" stroke-width="1"/>
  <text x="600" y="485" text-anchor="middle" fill="#888" font-size="11" font-weight="bold">SENTIMENT DETECTION OUTPUT → AI RESPONSE ADAPTATION</text>

  <!-- ANGRY -->
  <rect x="68" y="495" width="130" height="60" rx="8" fill="#1e1015" stroke="#ef4444" stroke-width="1.5"/>
  <text x="133" y="518" text-anchor="middle" fill="#ef4444" font-size="13">😡</text>
  <text x="133" y="533" text-anchor="middle" fill="#ef4444" font-size="10" font-weight="bold">ANGRY</text>
  <text x="133" y="547" text-anchor="middle" fill="#888" font-size="9">Apologize first</text>

  <!-- FRUSTRATED -->
  <rect x="210" y="495" width="130" height="60" rx="8" fill="#1e1510" stroke="#f97316" stroke-width="1.5"/>
  <text x="275" y="518" text-anchor="middle" fill="#f97316" font-size="13">😤</text>
  <text x="275" y="533" text-anchor="middle" fill="#f97316" font-size="10" font-weight="bold">FRUSTRATED</text>
  <text x="275" y="547" text-anchor="middle" fill="#888" font-size="9">Extra patience</text>

  <!-- HAPPY -->
  <rect x="352" y="495" width="130" height="60" rx="8" fill="#0f1e10" stroke="#22c55e" stroke-width="1.5"/>
  <text x="417" y="518" text-anchor="middle" fill="#22c55e" font-size="13">😊</text>
  <text x="417" y="533" text-anchor="middle" fill="#22c55e" font-size="10" font-weight="bold">HAPPY</text>
  <text x="417" y="547" text-anchor="middle" fill="#888" font-size="9">Match energy</text>

  <!-- CONFUSED -->
  <rect x="494" y="495" width="130" height="60" rx="8" fill="#0f1520" stroke="#3b82f6" stroke-width="1.5"/>
  <text x="559" y="518" text-anchor="middle" fill="#3b82f6" font-size="13">😕</text>
  <text x="559" y="533" text-anchor="middle" fill="#3b82f6" font-size="10" font-weight="bold">CONFUSED</text>
  <text x="559" y="547" text-anchor="middle" fill="#888" font-size="9">Simple language</text>

  <!-- NEUTRAL -->
  <rect x="636" y="495" width="130" height="60" rx="8" fill="#1a1a1a" stroke="#64748b" stroke-width="1.5"/>
  <text x="701" y="518" text-anchor="middle" fill="#64748b" font-size="13">😐</text>
  <text x="701" y="533" text-anchor="middle" fill="#64748b" font-size="10" font-weight="bold">NEUTRAL</text>
  <text x="701" y="547" text-anchor="middle" fill="#888" font-size="9">Default tone</text>

  <!-- LANGUAGES -->
  <rect x="778" y="495" width="360" height="60" rx="8" fill="#12101e" stroke="#8b5cf6" stroke-width="1.5"/>
  <text x="958" y="515" text-anchor="middle" fill="#8b5cf6" font-size="10" font-weight="bold">🌐 AUTO LANGUAGE DETECTION</text>
  <text x="958" y="533" text-anchor="middle" fill="#FFFFFF" font-size="11">🇮🇳 Hindi &nbsp;&nbsp; 🇮🇳 Marathi &nbsp;&nbsp; 🇮🇳 Tamil &nbsp;&nbsp; 🇮🇳 Telugu &nbsp;&nbsp; 🇬🇧 English</text>
  <text x="958" y="549" text-anchor="middle" fill="#888" font-size="9">Gemini auto-detects &amp; replies in customer's language</text>

</svg>




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

```

---

## 📸 Workflow Screenshot

<img width="1679" height="591" alt="image" src="https://github.com/user-attachments/assets/a3eb7a16-2c03-45ef-9f17-fcc8615760b7" />


---

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
