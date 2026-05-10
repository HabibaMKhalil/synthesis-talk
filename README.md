# SynthesisTalk

A full-stack AI assistant for document analysis and conversational chat. Upload PDFs or text files, get instant summaries and key points, and continue the conversation with an LLM that can also search the web.

## Features

- **Document Analysis** — Upload PDFs or `.txt` files, then summarize or extract key points using AI
- **Conversational Chat** — Multi-turn chat with session history, stored locally per user
- **Web Search Toggle** — Augment AI responses with live Google search results via SerpAPI
- **Authentication** — Email/password sign-up with email verification, plus guest mode (Firebase Auth)
- **Chat History** — Browse, rename, and delete past chat sessions from the sidebar

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 19, React Router, Tailwind CSS |
| Auth | Firebase Authentication |
| Backend | FastAPI + Uvicorn (Python) |
| LLM | Groq API (`llama-3.3-70b-versatile`) |
| PDF Parsing | PyMuPDF |
| Web Search | SerpAPI |

## Project Structure

```
SynthesisTalk/
├── synthesistalk-frontend/   # React app
│   └── src/
│       ├── pages/            # Login, Signup, Chat, Profile, Landing
│       ├── chatService.js    # API client
│       ├── chatStorage.js    # localStorage chat history
│       └── firebase.js       # Firebase config
└── synthesistalk-backend/
    └── main.py               # FastAPI endpoints
```

## Getting Started

### Backend

```bash
cd synthesistalk-backend
pip install fastapi uvicorn pymupdf python-dotenv aiofiles requests
```

Create a `.env` file:

```env
GROQ_API_KEY=your_groq_api_key
GROQ_MODEL=llama-3.3-70b-versatile
GROQ_BASE_URL=https://api.groq.com/openai/v1
MODEL_SERVER=GROQ
SERPAPI_KEY=your_serpapi_key
```

```bash
uvicorn main:app --reload
```

### Frontend

```bash
cd synthesistalk-frontend
npm install
npm start
```

The app runs at `http://localhost:3000` and expects the backend at `http://localhost:8000`.

## API Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| POST | `/api/upload` | Upload a file and create a session |
| POST | `/api/analyze` | Summarize or extract key points |
| POST | `/api/chat` | Send a message, get an LLM response |

## Notes

- Chat history is persisted in the browser's `localStorage` — no backend database required
- Firebase credentials in the frontend config should be restricted before going to production
- CORS is fully open (`*`) — lock it down for any deployed environment
