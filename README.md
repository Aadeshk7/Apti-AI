# APTI AI

APTI AI is an aptitude-training platform that combines a modern Vite + React interface with a Node.js API for AI-generated questions, streak sessions, and performance analysis. It supports Gemini-based generation, a local-model fallback pipeline, and dataset utilities for fine-tuning and experimentation.

## Key Features

- AI-generated aptitude questions (Quant, Verbal, LR, DI)
- Streak/batch generation with topic and difficulty controls
- Performance analysis with actionable recommendations
- Custom prompt generation and tutor-style chat endpoint
- Local model fallback via adapter-based LoRA pipeline
- Dataset creation from PDFs using Gemini

## Tech Stack

- Frontend: Vite, React, Tailwind CSS, GSAP, Recharts
- Backend: Node.js, Express, SQLite, Gemini API
- Python: Dataset extraction and generation utilities

## Project Structure

- src/: React UI
- backend/: Express API, SQLite DB, generators
- apti-llm/: Adapter artifacts and checkpoints
- main.py: PDF-to-dataset pipeline
- final_dataset.json: Example generated dataset

## Quick Start

### 1) Frontend

```bash
npm install
npm run dev
```

Vite prints the local URL (usually http://localhost:5173).

### 2) Backend

```bash
cd backend
npm install
node server.js
```

API runs on http://localhost:5000 by default.

### 3) Local Model Fallback (Optional)

The backend can attempt a local Python generator. This is a minimal stub in:
backend/run_local_model.py

To use a full local model, install PyTorch/Transformers and load the adapter in that script.

### 4) Dataset Pipeline (Optional)

```bash
pip install pymupdf google-generativeai
python main.py <path/to/apti.pdf>
```

The script generates final_dataset.json in the project root.

## Configuration

Create backend/.env if you do not already have one. Supported variables:

- GEMINI_API_KEY: API key for Gemini
- PORT: Backend port (default 5000)

For the Python pipeline:

- APTI_MODEL: Gemini model id (default models/gemini-2.0-flash)
- APTI_PDF_PATH: Single PDF path
- APTI_PDF_PATHS: Semicolon-separated PDF paths
- APTI_CHUNK_LIMIT: Max chunks processed per run (default 20)

## API Endpoints (Backend)

- GET /api/question
- POST /api/streak
- POST /api/analyze-streak
- POST /api/generate-custom
- POST /api/chat
- POST /api/user/sync
- POST /api/user/add-xp
- GET /api/leaderboard

## Notes

- The local model path and adapter assets live under apti-llm/.
- The backend uses SQLite for user profiles and XP tracking.

## License

MIT (update if different)
