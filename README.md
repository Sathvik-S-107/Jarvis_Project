# 🔊 Jarvis Voice Assistant

A Python-based Jarvis voice assistant that responds to voice commands, opens websites, plays music, fetches news, and uses AI (Mistral via Ollama) for smart replies.

---

## 🚀 Features
- Wake-word detection — "Jarvis"
- Speech-to-text using Google API
- Text-to-speech using pyttsx3
- AI chatbot replies using Mistral (Ollama)
- Open websites (Google, YouTube, Facebook, LinkedIn)
- Play songs from preset library
- Fetch top US news headlines

---

## 🛠️ Tech Used
| Component | Library |
|----------|---------|
| Speech Recognition | speech_recognition |
| Text to Speech | pyttsx3 |
| AI Model | ollama (Mistral) |
| Networking | requests |
| Browser | webbrowser |

---

## 📁 Project Structure
jarvis-voice-assistant/
│
├── jarvis.py
├── requirements.txt
└── README.md

---

## 📦 Installation

1️⃣ Clone the repository  
git clone https://github.com/<your-username>/jarvis-voice-assistant.git  
cd jarvis-voice-assistant  

2️⃣ Install dependencies  
pip install -r requirements.txt  

---

## 🤖 Setup Ollama

Download Ollama → https://ollama.com  

Pull Mistral model:  
ollama pull mistral  

---

## 🔑 News API Key
Get API key from https://newsapi.org/

Inside jarvis.py, replace:
newsapi = "YOUR_API_KEY"

---

## ▶️ Run the assistant
python jarvis.py

Say:
"Jarvis"

Then speak your command.

---

## 🎙️ Example Commands
| Command | Result |
|--------|--------|
| Jarvis → open google | Opens Google |
| Jarvis → play believer | Plays music |
| Jarvis → news | Reads news headlines |
| Jarvis → Who is Elon Musk? | AI reply |
| Jarvis → Tell me a joke | AI reply |

---

## 🔮 Future Improvements
- Reminders + alarms
- Email / WhatsApp support
- Full music streaming
- System control (brightness, volume)
- GUI interface

---

## 🧑‍💻 Author
Sathvik S  
GitHub: https://github.com/sathviks

---


