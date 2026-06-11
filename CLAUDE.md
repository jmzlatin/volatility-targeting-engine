# CLAUDE.md

## Project Purpose

A Volatility Targeting Position Sizing Engine that automatically downscales asset exposure during high-volatility periods and expands exposure during low-volatility periods based on a fixed risk constant.

## Architecture Boundaries

Maintain strict separation between three layers. Do not mix their responsibilities.

- **Data layer** (`data/`): Handles ingestion, caching, and cleaning of price series via yfinance. No math beyond returns calculation. No UI code.
- **Risk layer** (`risk/`): Pure mathematical functions for volatility estimation and weight calculation. Accepts and returns NumPy arrays or pandas objects. No data fetching. No Streamlit imports.
- **Frontend layer** (`app/`): Streamlit rendering, charts, and user inputs only. Calls into the data and risk layers. Contains no risk math and no direct yfinance calls.

A function in one layer must not import from a layer it does not own. The frontend calls data and risk. The risk layer stays pure and importable in isolation.

## Commands

Set up the virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Run the Streamlit app:

```bash
streamlit run app/main.py
```

Execute unit tests:

```bash
pytest
```

Run a single test file:

```bash
pytest tests/test_risk.py -v
```

## Workflow Constraints

- Read `tasks.md` at the start of every session before any other action. It defines current objectives and progress.
- Do not initiate code changes without consulting `tasks.md` first.
- Update `tasks.md` as work progresses. Mark completed items and add new tasks discovered during development.
- Keep `tasks.md` accurate. It is the source of truth for project state.
