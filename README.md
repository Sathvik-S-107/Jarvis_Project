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
## FINAL CODE
``` 
import speech_recognition as sr
import webbrowser
import pyttsx3
import requests
import ollama

recognizer = sr.Recognizer()
engine = pyttsx3.init()
newsapi = "f7bfee46fead478c84e9354c9cc182e4"

def speak(text):
    print("Jarvis:", text)
    try:
        engine = pyttsx3.init(driverName='sapi5')
        voices = engine.getProperty('voices')
        engine.setProperty('voice', voices[0].id)
        engine.setProperty('rate', 170)
        engine.say(text)
        engine.runAndWait()
        engine.stop()
    except Exception as e:
        print("🔇 TTS Error:", e)

def aiProcess(command):
    print("🧠 Sending to AI:", command)
    try:
        response = ollama.chat(
            model='mistral',
            messages=[{"role": "user", "content": command}]
        )
        return response['message']['content']
    except Exception as e:
        print("Ollama AI Error:", e)
        return "Sorry, I couldn't process that."

def processCommand(c):
    c = c.lower().strip().replace("\\", "")

    if 'open google' in c:
        webbrowser.open("https://google.com")
    elif 'open youtube' in c:
        webbrowser.open("https://youtube.com")
    elif 'open linkedin' in c:
        webbrowser.open("https://linkedin.com")
    elif 'open facebook' in c:
        webbrowser.open("https://facebook.com")

    elif c.startswith('play'):
        song = c.partition("play")[2].strip().lower()
        music = {
            "hotel california": "https://youtu.be/EqPtz5qN7HM",
            "rickroll": "https://youtu.be/dQw4w9WgXcQ",
            "bohemian rhapsody": "https://youtu.be/fJ9rUzIMcZQ",
            "back in black": "https://youtu.be/pAgnJDJN4VA",
            "believer": "https://youtu.be/7wtfhZwyrcc",
            "shape of you": "https://youtu.be/JGwWNGJdvx8",
            "perfect": "https://youtu.be/2Vv-BfVoq4g"
        }
        link = music.get(song)
        if link:
            speak(f"Playing {song}")
            webbrowser.open(link)
        else:
            speak(f"Sorry, I couldn't find the song {song} in my library.")

    elif "news" in c:
        speak("Fetching today's headlines...")
        r = requests.get(f"https://newsapi.org/v2/top-headlines?country=us&apiKey={newsapi}")
        if r.status_code == 200:
            data = r.json()
            articles = data.get('articles', [])[:5]
            for article in articles:
                speak(article['title'])
        else:
            speak("Failed to fetch news.")

    else:
        speak("Thinking...")
        output = aiProcess(c)
        speak(output)

if __name__ == '__main__':
    speak('Initializing Jarvis...')
    while True:
        r = sr.Recognizer()
        print('🎤 Listening for wake word...')

        try:
            with sr.Microphone() as source:
                recognizer.adjust_for_ambient_noise(source)
                print('Listening...')
                audio = recognizer.listen(source, timeout=5, phrase_time_limit=3)

            word = recognizer.recognize_google(audio)
            print("You said:", word)

            if word.lower() == "jarvis":
                speak('Yes?')
                with sr.Microphone() as source:
                    recognizer.adjust_for_ambient_noise(source)
                    print('🎤 Listening for command...')
                    audio = recognizer.listen(source, timeout=5, phrase_time_limit=5)
                    command = recognizer.recognize_google(audio)
                    command = command.strip().replace("\\", "")
                    print("Command:", command)
                    processCommand(command)

        except sr.WaitTimeoutError:
            print("⏱️ Timeout: No speech detected.")
        except sr.UnknownValueError:
            print("🗣️ Speech was unclear or not understood.")
        except sr.RequestError as e:
            print("🌐 Google Speech API error:", e)
        except Exception as e:
            print("⚠️ Unexpected error:", repr(e))

```


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


