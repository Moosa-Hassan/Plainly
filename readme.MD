# Plainly (NoJargon)

Plainly is a two-service app: a FastAPI backend that simplifies text, and a Streamlit frontend for a simple UI.

## Requirements
- Docker and Docker Compose (recommended for quickest start)
- Or: Python 3.10+ with pip if running locally

## Quick start (Docker)
1) Build and run both services:
	 ```bash
	 docker compose up --build
	 ```
2) Open the frontend at http://localhost:8501
3) Backend will be available at http://localhost:8000
4) To close and end both services:
    ```bash
    CTRL+C
    CTRL+C
    docker compose down
    ```

## Environment variables
- Backend uses `backend/.env` if present (loaded by compose). Add any keys (e.g., API tokens) there.
- Frontend talks to backend via `BACKEND_URL` (set in compose to `http://backend:8000`). Override locally if needed:
	```bash
	BACKEND_URL=http://localhost:8000 streamlit run app.py
	```

## Local dev without Docker
Backend:
```bash
cd backend
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

Frontend (new shell):
```bash
cd frontend
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
BACKEND_URL=http://localhost:8000 streamlit run app.py
```

## Useful endpoints
- POST /explain — body: `{ "text": "string", "mode": "very_simple|simple|normal" }`

## Troubleshooting
- If Docker on Windows cannot connect to the daemon, open Docker Desktop and ensure it is running.
- Port conflicts: change the published ports in docker-compose.yml (e.g., `8502:8501`).