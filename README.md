# 🔧 Automations & Media Tools Portfolio

> *“From low‑code vendor governance to an AI‑powered photo library, here’s how I build pragmatic solutions that save teams hours every week.”*

---

## 📑 Table of Contents
1. [Vendor Risk Assessment Bot](#-1-vendor-risk-assessment-bot-n8n--slack)
2. [Vendor Lookup / License Tracker](#-2-vendor-lookup--license-tracker-n8n--slack)
3. [AI Photo & Video Organizer](#-3-ai-photo--video-organizer-python-gui)
4. [Running Locally](#-running-each-project-locally)
5. [Folder Structure](#-folder-structure)
6. [License](#-license)

---

## 🚀 1  Vendor Risk Assessment Bot (N8N ↔ Slack)

| &nbsp; | Details |
| :- | :- |
| **Slash command** | `/assess <vendor>` |
| **LLM** | OpenChat 3.5 / DeepSeek‑R1 |
| **Context** | ISO 27001, SOC 2, GDPR + internal *Vendor Risk Guidelines* (fetched from Google Docs) |
| **Output** | Single Slack thread: *Overview → Compliance → Risks → Gaps → Recommendations* |

<details>
<summary><strong>Workflow walk‑through</strong></summary>

1. **`Webhook1`** – receives the Slack command  
2. **`Extract Vendor Name`** – parses the vendor string  
3. **`Fetch Policies`** – pulls the latest policy doc from Google Docs  
4. **`Build AI Prompt`** – crafts system + user messages  
5. **`OpenAI1`** – calls the LLM  
6. **`Extract Assessment`** – unwraps the JSON response  
7. **`Slack`** – posts the formatted block back to the channel  
</details>

### Import & Run

```bash
# import the workflow (or paste JSON in the n8n editor)
n8n import:workflow n8n-workflows/vendor-risk-assessment-2.0.json

# set credentials
#  • Slack Bot token
#  • Google Docs OAuth
#  • OpenAI / DeepSeek API key

# then in Slack:
# /assess HubSpot
