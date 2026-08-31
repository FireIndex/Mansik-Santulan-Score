# Mansik Santulan Score

**Mental Health Signal** — a student wellness predictor that estimates a mental health score (0–10) from screen-time, academic, and lifestyle habits. It pairs a scikit-learn regression model with a FastAPI backend and a static HTML/CSS/JS frontend.

> Built for informational purposes only — this is not a clinical assessment.

## How it works

1. A visitor fills out a form (age, gender, country, academic level, social media platform/purpose, screen time, phone unlocks, study/activity/sleep hours, stress level).
2. The frontend (`index.html`, `style.css`, `script.js`) sends the data to a FastAPI backend.
3. The backend (`main.py`) loads a trained model (`Mental_Health_Model.pkl`) and returns a predicted mental health score.

## Project structure

| File | Purpose |
|---|---|
| `main.py` | FastAPI app — `/predict` endpoint that runs the model |
| `Mental_Health_Model.pkl` | Trained scikit-learn model, loaded via `joblib` |
| `ML_Project.ipynb` | Notebook with data exploration and model training |
| `Student Social Media And Mental Health Impact.csv` | Training dataset |
| `index.html`, `style.css`, `script.js` | Frontend UI |
| `pyproject.toml` / `uv.lock` | Python dependencies (managed with [uv](https://docs.astral.sh/uv/)) |

## Running locally

### Backend

```bash
uv sync
uv run uvicorn main:app --reload
```

The API will be available at `http://127.0.0.1:8000`, with interactive docs at `/docs`.

### Frontend

Open `index.html` in a browser, or serve the folder with any static file server. By default it calls the deployed API at `API_BASE` in `script.js` — update that constant to point at your local backend if needed.

## API

### `POST /predict`

Request body:

```json
{
  "age": 21,
  "gender": "Male",
  "country": "India",
  "academic_level": "Undergraduate",
  "most_used_platform": "Instagram",
  "purpose_of_use": "Entertainment",
  "avg_daily_usage_hours": 4.5,
  "daily_unlocks": 60,
  "study_hours": 3,
  "physical_activity_hours": 1,
  "sleep_hours_per_night": 6.5,
  "stress_level": "Medium"
}
```

Response:

```json
{
  "predicted_mental_health_score": 6.78
}
```

## Deployment

The backend is deployed on Render at `https://mansik-santulan-score-8uyo.onrender.com`.
