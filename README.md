# rental-price-prediction-rest-api
Airbnb Rental Price Prediction - Flask API Backend + Streamlit Frontend (Dockerized)

## Requirements

The model (`backend/rental_price_prediction_model_v1_0.joblib`) was saved with **scikit-learn 1.6.1**, so it must be loaded with the same version. scikit-learn 1.6.1 supports Python 3.9–3.12; on Python 3.13+ the pinned version can't install and loading fails with errors such as:

```
AttributeError: module 'sklearn.compose._column_transformer' has no attribute '_RemainderColsList'
```

The dev container and Dockerfiles in this repo use **Python 3.12**.

## Run in GitHub Codespaces

Create a new Codespace from this repo. It uses `.devcontainer/devcontainer.json` (Python 3.12 + Docker) and installs both requirements files automatically.

> An existing Codespace created before the dev container was added keeps its old Python. Run **Codespaces: Rebuild Container** from the command palette, or create a new Codespace.

### Option A: Docker Compose

```bash
docker compose up --build
```

### Option B: Run both apps directly

Terminal 1 (backend on port 7860):

```bash
cd backend && python app.py
```

Terminal 2 (frontend on port 8501):

```bash
cd frontend && streamlit run app.py --server.enableXsrfProtection=false
```

Open the forwarded port **8501** to use the app.

## API

- `GET /` - health check
- `POST /v1/rental` - JSON body with `room_type`, `accommodates`, `bathrooms`, `cancellation_policy`, `cleaning_fee`, `instant_bookable`, `review_scores_rating`, `bedrooms`, `beds`
- `POST /v1/rentalbatch` - CSV upload (`file`) with the same columns plus `id`
