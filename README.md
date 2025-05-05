🔧 Automations & Media Tools Portfolio

“From low‑code vendor governance to an AI‑powered photo library, here’s how I build pragmatic solutions that save teams hours every week.”

⸻

📑 Table of Contents
	1.	Vendor Risk Assessment Bot
	2.	Vendor Lookup / License Tracker
	3.	AI Photo & Video Organizer
	4.	Running Locally
	5.	Folder Structure
	6.	License

⸻

🚀 1  Vendor Risk Assessment Bot (N8N ↔ Slack)

  	 Details
Slash command	/assess <vendor>
LLM	 OpenChat 3.5 / DeepSeek‑R1
Context	ISO 27001, SOC 2, GDPR + internal “Vendor Risk Guidelines” (pulled live from Google Docs)
Output	Single Slack thread: Overview → Compliance → Risks → Gaps → Recommendations

<details>
<summary>Workflow walk‑through</summary>


	1.	Webhook1 – receives the Slack command.
	2.	Extract Vendor Name – parses text for the vendor string.
	3.	Fetch Policies – grabs the latest policy doc from Google Docs.
	4.	Build AI Prompt – crafts system + user messages.
	5.	OpenAI1 – calls the LLM.
	6.	Extract Assessment – unwraps the JSON response.
	7.	Slack – posts the formatted block back to the channel.

</details>


### Import & run

# import the JSON (or paste into n8n GUI)
n8n import:workflow n8n-workflows/vendor-risk-assessment-2.0.json

# set credentials
#  – Slack Bot token
#  – Google Docs OAuth
#  – OpenAI / DeepSeek API key

# press ▶︎ Execute Workflow, then in Slack:
/assess HubSpot



⸻

🔍 2  Vendor Lookup / License Tracker (N8N ↔ Slack)

A single source‑of‑truth Google Sheet + fuzzy search + interactive Slack blocks.
	•	Exact + Levenshtein matching (Exact‑Fuzzy node).
	•	Dynamic Blocks API rendering (Format Response node).
	•	“Request More Info” button opens a secondary workflow that fetches and posts deeper details in‑thread.

### Import & run

n8n import:workflow n8n-workflows/vendor-workflow-prototype.json
# add Google Sheets + Slack creds
# trigger: /vendor Okta   (or any supplier name)



⸻

🖼 3  AI Photo & Video Organizer (Python GUI)

<p align="center"><img src="assets/organiser_screenshot.png" width="500"></p>


Desktop app that:
	•	Scans any folder or drive for photos and videos
	•	Reads EXIF / video metadata → auto‑sorts into …/YYYY/MM/
	•	Detects duplicates with perceptual hashing (images) or multi‑frame MD5 (videos)
	•	Live progress bar, cancel button, and end‑of‑run stats

### Quick start

# 1. set up env
python -m venv .venv && source .venv/bin/activate
pip install -r python-media-organiser/requirements.txt

# 2. launch GUI
python python-media-organiser/organise_media.py



⸻

⚙️ Running each project locally

Project	Prerequisites	One‑liner
N8N workflows	Docker or npm i -g n8n · Slack App · Google API creds · OpenAI key	docker run -p 5678:5678 -v ~/.n8n:/home/node/.n8n n8nio/n8n
Media Organizer	Python ≥ 3.9	python organise_media.py <source> <target>



⸻

📂 Folder Structure

.
├── n8n-workflows/
│   ├── vendor-risk-assessment-2.0.json
│   └── vendor-workflow-prototype.json
├── python-media-organiser/
│   ├── organise_media.py
│   └── requirements.txt
├── assets/
│   ├── risk_assessment_demo.gif
│   ├── vendor_lookup_demo.gif
│   └── organiser_screenshot.png
└── README.md



⸻

🪪 License

Released under the MIT License. Feel free to clone, fork, and build on top of these automations—just drop me a note if you ship something cool!

⸻

✉️ Questions / Feedback?

Open an issue or reach me at venzdanao03@gmail.com. I love talking automation, security, and Python performance tricks.
