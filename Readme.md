# 🧠 AI Persona – Chat with Hitesh Choudhary (Gemini AI Clone)

An interactive web-based chatbot that mimics the **personality, tone, and storytelling style** of a real person. In this project, I've cloned the essence of **Hitesh Choudhary**, but you can swap the persona for **any creator, founder, or even yourself!**

## 🧰 Tools You'll Need

- **🧠 Gemini API (Google Generative AI)** – For generating responses using Gemini models  
- **🌐 Streamlit** – For building a fast, clean web UI  
- **🔐 python-dotenv** – For loading environment variables securely  
- **💻 Python (>=3.8)** – Your core programming language

## 📁 Project Structure



```
ai-persona/
├── persona.py # Main Streamlit app
├── .env # Store your Gemini API key
├── prompts/
│ └── hitesh_examples.json # ~40 examples of how Hitesh speaks
├── requirements.txt
└── README.md
```

## 🧱 Step-by-Step Build

### 1️⃣ Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

### 2️⃣ Install Dependencies

```
pip install streamlit google-generativeai python-dotenv
```

### 3️⃣ Add Your API Key

Create a `.env` file:

```env
GEMINI_API_KEY=your-gemini-api-key-here
```

### 4️⃣ Prompt Engineering is the 💖

To simulate Hitesh Choudhary's unique style:

- Transcripts from 2-3 YouTube videos
- Insights from LinkedIn, Udemy courses
- Tone: Hinglish, emotional, motivational, storytelling

Example prompt:

```json
{
  "role": "user",
  "content": "Hitesh bhai, mujhe backend seekhna hai par kahan se start karu?"
},
{
  "role": "assistant",
  "content": "Bilkul, backend seekhna kaafi exciting journey hai. Dekho sabse pehle Node.js ya Python choose karo..."
}
```

### 5️⃣ Main Streamlit App (app.py)

```python
import streamlit as st
import google.generativeai as genai
from dotenv import load_dotenv
import os
import json

load_dotenv()
genai.configure(api_key=os.getenv("GEMINI_API_KEY"))
model = genai.GenerativeModel("gemini-pro")

SYSTEM_PROMPT = """
You are an AI version of Hitesh Choudhary.
You speak in Hinglish with storytelling flair, use simple analogies, 
emotional motivation, and break down tech concepts for learners. 
You are informal, encouraging, and sound like a relatable mentor.
"""

st.title("🤖 Chat with Hitesh Choudhary (AI)")

query = st.text_input("Aapka sawal?")

if query:
    with open("prompts/hitesh_examples.json", "r") as f:
        examples = json.load(f)
    
    history = [{"role": "user", "parts": SYSTEM_PROMPT}]
    
    for example in examples:
        history.append({"role": example["role"], "parts": example["content"]})

    history.append({"role": "user", "parts": query})

    response = model.generate_content(history)
    st.write(response.text)
```

### 6️⃣ Run the App 🚀

```bash
streamlit run persona.py
```


**Boom 💥** — your own Hitesh AI clone is live!


## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](../../issues).

## 📞 Support

If you have any questions or need help, please open an issue or reach out on Twitter.

---

**Made with ❤️ and AI**
