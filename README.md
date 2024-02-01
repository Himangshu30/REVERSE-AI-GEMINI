# REVERSE-AI-GEMINI

# Gemini
Google Gemini AI model w/speech recognition and voice.

<br>

# Obtain API Key
[HERE](https://makersuite.google.com/app/apikey)

# Setup: Linux/MAC
### Add API Environment Variable `GOOGLE_GEMINI_API_KEY` [HERE](https://www.youtube.com/watch?v=5BTnfpIq5mI)
### Install ffmpeg [HERE](https://www.hostinger.com/tutorials/how-to-install-ffmpeg)
```bash
python3 -m venv venv
.\venv\Scripts\activate
pip install -r requirements.txt
```

# Setup: Windows
### Add API Environment Variable `GOOGLE_GEMINI_API_KEY`
```bash
export GOOGLE_GEMINI_API_KEY="<YOUR_GOOGLE_GEMINI_API_KEY>"
```
### Install ffmpeg [HERE](https://www.hostinger.com/tutorials/how-to-install-ffmpeg)
```bash
python3 -m venv venv
source venv/bin/active
pip install -r requirements.txt
```

# Usage: 
```bash
python gemini.py
```

# `gemini.py`
```python
import os
import subprocess
import pathlib
import textwrap
import google.generativeai as genai
from IPython.display import display, Markdown
from gtts import gTTS
import speech_recognition as sr

GOOGLE_GEMINI_API_KEY = os.environ['GOOGLE_GEMINI_API_KEY']
genai.configure(api_key=GOOGLE_GEMINI_API_KEY)
model = genai.GenerativeModel('gemini-pro')

while True:
	r = sr.Recognizer()
	mic = sr.Microphone()
	with mic as source:
		print("Speak now to Gemini...")
		audio = r.listen(source)
	text = r.recognize_google(audio)
	response = model.generate_content(text)
	speech = gTTS(response.text, lang='en')
	speech.save('output.mp3')
	process = subprocess.Popen(['ffplay', '-nodisp', '-autoexit', '-loglevel', 'quiet', 'output.mp3'],
		stdout=subprocess.DEVNULL,
		stderr=subprocess.DEVNULL)
	process.wait()
```

<br>
