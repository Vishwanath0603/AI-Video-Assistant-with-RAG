# 🎬 AI Video Assistant

> **Transcribe • Summarise • Extract Insights • Chat with Your Meetings**

An AI-powered meeting and video intelligence application that transforms YouTube videos or local audio/video files into searchable, structured insights.

The application combines **Whisper-based speech recognition**, **Mistral AI**, **LangChain**, **Hugging Face embeddings**, and **ChromaDB** to create an end-to-end pipeline for transcription, summarisation, insight extraction, and Retrieval-Augmented Generation (RAG) chat.

---

## ✨ Features

- 🎥 **YouTube & Local Media Input** — Process a YouTube URL or a local audio/video file.
- 🎙️ **Automatic Audio Processing** — Downloads, converts, and prepares media for transcription.
- 📝 **Speech-to-Text** — Uses OpenAI Whisper for local transcription.
- 🌐 **Language Support** — Supports English and Hinglish workflows.
- 🏷️ **Automatic Title Generation** — Generates a concise professional title from the transcript.
- 📋 **AI Meeting Summarisation** — Produces a structured summary of long-form conversations.
- ✅ **Action Item Extraction** — Identifies tasks, owners, and deadlines when available.
- 🔑 **Key Decision Extraction** — Extracts important decisions made during the meeting.
- ❓ **Open Question Extraction** — Identifies unresolved questions and follow-up topics.
- 🧠 **RAG-Based Chat** — Ask questions about the processed meeting using retrieved transcript context.
- 💬 **Interactive Chat Interface** — Continue asking questions about the current meeting.
- 📊 **Live Pipeline Status** — Shows the progress of audio processing, transcription, title generation, summarisation, extraction, and RAG setup.
- 🎨 **Modern Streamlit UI** — Dark, responsive interface designed for meeting intelligence.

---

## 🖥️ Application Preview

### Initial Screen

![AI Video Assistant](screenshots/home.png)

### Meeting Analysis

![Meeting Analysis](screenshots/analysis.png)

> **Note:** Add your two screenshots to a `screenshots` folder and name them `home.png` and `analysis.png` to display them here.

---

## 🔄 How It Works

```text
             YouTube URL / Local Media
                       │
                       ▼
               Audio Processing
                       │
                       ▼
                 Audio Chunking
                       │
                       ▼
              Whisper Transcription
                       │
                       ▼
              Title Generation
                       │
                       ▼
                AI Summarisation
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
        Action Items Decisions  Questions
             │         │         │
             └─────────┼─────────┘
                       ▼
              Transcript Chunking
                       │
                       ▼
             Hugging Face Embeddings
                       │
                       ▼
                  ChromaDB
                       │
                       ▼
                 Retriever
                       │
                       ▼
               Mistral AI + RAG
                       │
                       ▼
                  Chat / Q&A
```

The application first converts the input media into audio, generates a transcript, and then uses the transcript for downstream analysis. The RAG pipeline splits the transcript into chunks, creates embeddings, stores them in ChromaDB, retrieves relevant context, and passes that context to Mistral AI for grounded answers.

---

## 🧠 RAG Pipeline

The RAG component is designed to answer questions **using the processed meeting transcript as context**.

### Pipeline

1. Transcript is generated from the input media.
2. Transcript is split into smaller chunks.
3. Hugging Face/Sentence Transformers generate vector embeddings.
4. Embeddings are stored in a local ChromaDB vector store.
5. Relevant transcript chunks are retrieved for each question.
6. Mistral AI receives the retrieved context and user question.
7. The assistant generates a concise answer grounded in the transcript.

This reduces the need to pass the entire transcript to the model for every question and makes long-form meeting content easier to query.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **Python** | Core application development |
| **Streamlit** | Interactive web application |
| **OpenAI Whisper** | Local speech-to-text |
| **yt-dlp** | YouTube media acquisition |
| **PyDub** | Audio manipulation and conversion |
| **FFmpeg** | Audio/video processing |
| **LangChain** | LLM and RAG orchestration |
| **Mistral AI** | Title generation, summarisation, extraction and Q&A |
| **Sentence Transformers** | Text embeddings |
| **Hugging Face** | Embedding/model ecosystem |
| **ChromaDB** | Local vector database |
| **PyTorch / Torchaudio** | Whisper backend and audio utilities |
| **Python-dotenv** | Environment variable management |

The current project requirements include Whisper, PyTorch, yt-dlp, FFmpeg bindings, LangChain/Mistral integrations, ChromaDB, Sentence Transformers, Streamlit, and related utilities. citeturn4view0

---

## 📁 Project Structure

```text
AI-Video-Assistant-
│
├── app.py
├── main.py
├── test.py
├── Requirements.txt
├── .gitignore
│
├── core/
│   ├── transcriber.py
│   ├── summarizer.py
│   ├── extractor.py
│   ├── rag_engine.py
│   └── vector_store.py
│
└── utils/
    └── audio_processor.py
```

The repository currently contains separate modules for transcription, summarisation, extraction, RAG, vector storage, and audio processing. citeturn1view0turn1view1

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/Vishwanath0603/AI-Video-Assistant-with-RAG.git
cd AI-Video-Assistant-with-RAG
```

Because the current repository contains the application one level below the repository root, enter the project directory:

```bash
cd "Video Assistant with rag/AI-Video-Assistant-"
```

### 2. Create a virtual environment

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

#### macOS / Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Python dependencies

```bash
pip install -r Requirements.txt
```

---

## 🎞️ FFmpeg Setup

FFmpeg is required for audio/video processing.

Verify that FFmpeg is available:

```bash
ffmpeg -version
```

If the command is not recognized, install FFmpeg and add it to your system `PATH`.

---

## 🔐 Environment Variables

Create a `.env` file in the project directory.

```env
MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key
WHISPER_MODEL=small
SARVAM_STT_MODEL=saaras:v2.5
```

### Important

Never commit your `.env` file or API keys to GitHub.

The application reads the Mistral API key for the Mistral-powered analysis/RAG components, while the transcription module can use Sarvam for its translation workflow. citeturn5view0turn5view1

---

## ▶️ Run the Application

Start the Streamlit interface:

```bash
streamlit run app.py
```

Then open the local URL displayed by Streamlit.

### Using the application

1. Enter a **YouTube URL** or **local media file path**.
2. Select the language:
   - `english`
   - `hinglish`
3. Click **⚡ Analyse**.
4. The pipeline processes the media.
5. Review:
   - Generated session title
   - Meeting summary
   - Full transcript
   - Action items
   - Key decisions
   - Open questions
6. Use **RAG Chat** to ask questions about the meeting.

The Streamlit application exposes YouTube/local-file input, English/Hinglish selection, and the analysis pipeline shown in the UI. citeturn3view4

---

## 🧩 Pipeline Components

### 1. Audio Processing

The application accepts YouTube URLs or local media paths and prepares the audio for downstream processing.

### 2. Transcription

Whisper is used for local speech recognition. The project also contains a Sarvam speech-to-text/translation workflow for supported language processing. citeturn5view1

### 3. AI Analysis

The transcript is passed through several LLM-powered tasks:

- Professional meeting title generation
- Meeting summarisation
- Action-item extraction
- Key-decision extraction
- Open-question extraction

These tasks are implemented using LangChain and Mistral AI. citeturn6view0turn6view1

### 4. Retrieval-Augmented Generation

The transcript is converted into embeddings and stored in ChromaDB. A retriever selects relevant transcript sections before the question is sent to the Mistral model. citeturn5view0

---

## 💡 Example Use Cases

### Meeting Intelligence
Turn long meetings into summaries, action items, decisions, and follow-up questions.

### YouTube Research
Analyse long-form YouTube content and ask questions about specific topics discussed in the video.

### Lectures & Learning
Convert educational videos into searchable transcripts and summaries.

### Interviews
Extract important discussion points, decisions, and unanswered questions from interviews.

### Webinars & Podcasts
Process long-form audio/video content and interact with it through RAG-based Q&A.

---

## 🚀 Future Improvements

- [ ] Support multiple video/audio files in one session
- [ ] Add speaker diarization
- [ ] Add timestamps to transcript-based answers
- [ ] Add downloadable PDF/Markdown reports
- [ ] Improve multilingual transcription
- [ ] Add persistent conversation history
- [ ] Add evaluation metrics for RAG responses
- [ ] Containerize with Docker
- [ ] Deploy the Streamlit application

---

## ⚠️ Notes

- Whisper models can require significant CPU/GPU resources depending on model size.
- FFmpeg must be installed separately from the Python packages.
- API keys should be stored in `.env` and never committed.
- RAG answers are grounded in retrieved transcript context; if the required information is not present in the transcript, the system is designed to indicate that it could not find the information.

---

## 👨‍💻 Author

**Vishwanath S**

GitHub: [@Vishwanath0603](https://github.com/Vishwanath0603)

---

## ⭐ Project

If you find this project useful, consider giving the repository a star.

**Repository:**  
https://github.com/Vishwanath0603/AI-Video-Assistant-with-RAG
