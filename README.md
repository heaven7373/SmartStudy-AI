# SmartStudy AI 📚

[![GitHub stars](https://img.shields.io/github/stars/heaven7373/SmartStudy-AI?style=flat-square)](https://github.com/heaven7373/SmartStudy-AI)
[![License](https://img.shields.io/github/license/heaven7373/SmartStudy-AI?style=flat-square)](LICENSE)

SmartStudy AI is a **Streamlit**-based web app that lets you upload your study materials (PDFs, Word docs, PowerPoints, images, etc.) and have an intelligent, conversational assistant answer questions **grounded only in your documents**. Powered by Google's Gemini models, it provides fast, accurate, and hallucination‑free responses.

---

## ✨ Features

- **Multi‑format support** – PDF, TXT, DOCX/DOC, PPTX/PPT, PNG/JPEG.
- **Zero‑hallucination** – The LLM only uses the uploaded document context.
- **Chunked embeddings** – Automatic text splitting and vector store creation with Chroma.
- **Robust retry logic** – Handles transient Gemini API errors (503, UNAVAILABLE, etc.).
- **Streamlit UI** – Clean, responsive, and fully customizable.
- **Live chat** – Ask follow‑up questions and retain conversation history.

---

## 🚀 Quick Start

### 1️⃣ Prerequisites

- **Python 3.10+**
- **Git** (to clone the repo)
- A **Google Gemini API key** (set `GOOGLE_API_KEY` in a `.env` file). See the [Gemini documentation](https://ai.google.dev/gemini-api) for details.

### 2️⃣ Clone the repository

```bash
git clone https://github.com/heaven7373/SmartStudy-AI.git
cd SmartStudy-AI/smartstudy-main
```

### 3️⃣ Install dependencies

```bash
python -m venv .venv
.venv\Scripts\activate   # on Windows
pip install -r requirements.txt
```

> **Tip**: The project uses a virtual environment located in `.venv` to keep dependencies isolated.

### 4️⃣ Configure environment variables

Create a `.env` file in the project root:

```dotenv
GOOGLE_API_KEY=YOUR_GEMINI_API_KEY
```

### 5️⃣ Run the app

```bash
streamlit run app.py
```

Open the URL shown in the terminal (usually `http://localhost:8501`).

---

## 📂 Project Structure

```
smartstudy-main/
├── .env                 # API keys (not committed)
├── .gitignore
├── app.py               # Streamlit entry‑point & core logic
├── requirements.txt     # Python dependencies
├── README.md            # **You are here!**
└── .streamlit/
    └── config.toml      # Streamlit configuration (theme, etc.)
```

---

## 🛠️ How It Works

1. **Upload Documents** – Select files via the sidebar.
2. **Extraction** – PDFs are read with `pypdf`, Word docs with `python-docx`, PPTX with `python-pptx`, and images are sent to Gemini’s vision model for OCR.
3. **Chunking** – Text is split into 1,000‑character chunks (200‑character overlap) using `RecursiveCharacterTextSplitter`.
4. **Embedding** – Each chunk is embedded with `GoogleGenerativeAIEmbeddings` and stored in a Chroma vector store.
5. **Query** – When you ask a question, the top‑k similar chunks are retrieved, combined into a prompt, and sent to `ChatGoogleGenerativeAI`.
6. **Answer** – The LLM returns a concise answer based only on the supplied context.

---

## 🎨 Customisation

- **Theme** – Edit `.streamlit/config.toml` to change the colour palette, fonts, or enable dark mode.
- **Prompt** – Modify the prompt template in `app.py` (lines 108‑124) to tweak the assistant’s tone or behaviour.
- **Model** – Switch `GoogleGenerativeAIEmbeddings` or `ChatGoogleGenerativeAI` to a different Gemini model if desired.

---

## 📸 Demo

![SmartStudy AI UI](https://raw.githubusercontent.com/heaven7373/SmartStudy-AI/main/assets/demo.png)

*The screenshot shows the sidebar for uploading documents and the chat interface for asking questions.*

---

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Ensure the code follows the existing style and passes linting.
4. Open a pull request with a clear description of your changes.

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

## 🙋‍♀️ Support

If you encounter any issues or have questions, feel free to open an issue on GitHub or reach out via the repository’s Discussions page.
