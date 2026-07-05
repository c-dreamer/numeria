# Numeria — Numerai Pipeline

Automated Numerai tournament pipeline — trains LightGBM models and submits predictions
to the Numerai main tournament, Crypto tournament, and Signals tournament.

Extracted from the `human-ai` monorepo.

## Pipelines

| Pipeline | Tournament | Script |
|----------|-----------|--------|
| Main | Numerai main tournament | `core/agents/numerai/numerai_pipeline.py` |
| Crypto | Numerai Crypto | `core/agents/numerai/crypto_pipeline.py` |
| Signals | Numerai Signals | `core/agents/numerai/signal_pipeline.py` |

## Quick Start

```bash
# Set up venv and install
python3 -m venv .venv && source .venv/bin/activate
pip install lightgbm numerapi pandas numpy scikit-learn joblib cloudpickle

# Dry run (uses synthetic data if no cache)
python3 core/agents/numerai/numerai_pipeline.py --dry-run

# Full run with submission
python3 core/agents/numerai/numerai_pipeline.py --model-id <your_model_id>
```

## Configuration

Create a `.env` file in the repo root:

```env
NUMERAI_PUBLIC_ID=your_public_id_here
NUMERAI_SECRET_KEY=your_secret_key_here
```

Model IDs are configured in `core/agents/numerai/models_config.json`.

## Daily Automation

Use `scripts/submit_all.py` to run all pipelines sequentially (designed for cron/systemd):

```bash
python3 scripts/submit_all.py
```

## Project Structure

```
numeria/
├── core/agents/numerai/       # Pipeline scripts and configs
│   ├── numerai_pipeline.py    # Main tournament
│   ├── crypto_pipeline.py     # Crypto tournament
│   ├── signal_pipeline.py     # Signals tournament
│   ├── utils.py               # Shared utilities
│   ├── models/                # Trained model artifacts
│   └── models_config.json     # Model IDs and configs
├── scripts/
│   └── submit_all.py          # Daily submission runner
└── agents/numerai -> core/agents/numerai  # Symlink for imports
```
