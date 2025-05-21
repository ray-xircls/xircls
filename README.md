# 🧠 XIRCLS: AI-Powered Meeting Transcription with Speaker Diarization

A Django web application that connects to **Microsoft Outlook** and **OneDrive** to fetch Teams meeting recordings, then transcribes them with **Whisper** and labels speakers with **Pyannote**.  
Everything is displayed in a clean web dashboard—one click, and you get a speaker-attributed transcript.

---

## 🚀 Features
- **OAuth 2.0** sign-in with Microsoft 365
- **Calendar view** of upcoming Outlook meetings
- **Automatic discovery** of Teams recordings in OneDrive ▸ “Recordings” folder
- **Whisper ASR** for high-quality speech-to-text
- **Pyannote Audio** for speaker diarization (who-said-what)
- **One-click transcription** button beside every recording
- **JSON API** endpoints for sentiment analysis & Vosk voice recognition (extras)

---

## 📂 Project Structure

XIRCLS/
├── outlook_integration/ # Microsoft Graph (login, calendar, OneDrive)
├── transcription/ # Whisper + Pyannote pipeline
├── sentiment/ # Example APIs (RoBERTa sentiment, Vosk STT)
├── templates/ # Django HTML files
├── vosk_model/ # (optional) offline Vosk model
├── manage.py
└── README.md

yaml
Copy
Edit

---

## 🧰 Tech Stack

| Layer | Technology |
|-------|------------|
| **Backend** | Django 5 · Django REST Framework |
| **Auth** | Microsoft Identity Platform (OAuth 2.0 PKCE) |
| **APIs** | Microsoft Graph (Calendars.Read, Files.Read.All) |
| **ASR** | Hugging Face Transformers — `openai/whisper-base` |
| **Diarization** | Pyannote Audio — `pyannote/speaker-diarization` |
| **Audio** | Pydub · ffmpeg |
| **DevOps** | Python 3.11 · venv · dotenv |

---

## ⚙️ Setup

1. **Clone & venv**
   ```bash
   git clone https://github.com/rl4658/XIRCLS.git
   cd XIRCLS
   python -m venv env && source env/bin/activate  # Windows: env\Scripts\activate
Install

bash
Copy
Edit
pip install -r requirements.txt
ffmpeg (required by pydub)

Ubuntu: sudo apt install ffmpeg

macOS: brew install ffmpeg

Windows: download from https://ffmpeg.org and add to PATH

Environment vars – create .env in the project root:

env
Copy
Edit
DJANGO_SECRET_KEY=replace_with_random_string
O365_CLIENT_ID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
O365_CLIENT_SECRET=your_msapp_secret
HUGGINGFACE_TOKEN=hf_XXXXXXXXXXXXXXXXXXXXXXXXXXXX
Migrate & run

bash
Copy
Edit
python manage.py migrate
python manage.py runserver
Open http://localhost:8000/outlook/ and sign in with your Microsoft account.

🔄 Workflow
Dashboard shows meetings & OneDrive recordings.

Click Transcribe → the MP3 is downloaded, converted to WAV (mono 16 kHz).

Pyannote assigns speaker segments.

Whisper transcribes audio to text with word-level timestamps.

Words are aligned to speaker turns → you get a clean, speaker-labeled transcript in the browser.

🖼️ Screenshots
Dashboard	Transcript

🧪 API Playground
Sentiment demo (RoBERTa):

bash
Copy
Edit
curl -X POST http://localhost:8000/api/sentiment/ \
     -H "Content-Type: application/json" \
     -d '{"text": "This project is awesome!"}'
📝 Troubleshooting
Issue	Fix
Pyannote access denied	Accept model license on HF & set HUGGINGFACE_TOKEN
ffmpeg not found	Confirm it’s in your PATH
Token expired	Delete o365_token.txt and re-login

📜 License
MIT – see LICENSE.

✨ Acknowledgements
OpenAI Whisper · Hugging Face · Pyannote Audio · Microsoft Graph · Vosk

👤 Author
Raymond Li — LinkedIn · Portfolio · GitHub
