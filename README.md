# Junction Lab

Junction Lab is a local college minor-project application for next-15-minute traffic forecasting, constrained signal-timing recommendations, deterministic intersection simulation, and fair controller comparison. It uses the City of Toronto turning-movement survey data already stored in this repository. It does not connect to live signals or claim field validation.

## Requirements

- Python 3.9 (the checked model artifacts were created with scikit-learn 1.6.1)
- Node.js 20 or newer
- npm

## Start locally

From the repository root:

```bash
python3.9 -m venv .venv
source .venv/bin/activate
python -m pip install -r backend/requirements.txt
python -m uvicorn backend.main:app --reload --host 127.0.0.1 --port 8000
```

In a second terminal:

```bash
cd frontend
npm install
npm run dev -- --host 127.0.0.1
```

Open `http://127.0.0.1:5173`. To use another API origin, set `VITE_API_ORIGIN` before starting Vite.

## Checks

```bash
source .venv/bin/activate
python -m unittest discover -s backend/tests -v
cd frontend
npm test
npm run lint
npm run build
```

## Reproduce preprocessing and a new model run

Raw data is never overwritten. Preprocessing writes the documented ML-ready table; training writes a timestamped directory under `backend/models/runs/` and leaves the checked baseline artifacts unchanged.

```bash
source .venv/bin/activate
python -m backend.scripts.prepare_ml_data
python -m backend.scripts.train_model
python -m backend.scripts.evaluate_model
```

Read [Architecture](docs/ARCHITECTURE.md), [Methodology](docs/METHODOLOGY.md), [Data Dictionary](docs/DATA_DICTIONARY.md), [Demo Guide](docs/DEMO_GUIDE.md), [Viva Notes](docs/VIVA_NOTES.md), and the [Project Report](report/PROJECT_REPORT.md).
# smart-traffic-signal-prediction
