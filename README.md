# OpenAI Agents — Memory Demo

A small Jupyter notebook that compares an OpenAI Agents SDK agent **without memory** vs. **with memory** (`SQLiteSession`), using a personal finance advisor as the example.

## What it shows

The same two queries are sent to the same agent twice:

1. `"I spent $120 on groceries, $40 on Uber, and $60 on restaurants this week."`
2. `"My weekly budget is $250. Based on everything I told you so far, where can I cut spending next week?"`

- **Without memory** — each `Runner.run` call is independent. Query 2 has no record of the expenses from query 1, so the agent asks the user to re-send them.
- **With memory** — a `SQLiteSession` is attached to both runs. Query 2 sees the full prior turn and gives concrete cuts grounded in the $220 total against the $250 budget.

## Run it

```powershell
python -m venv venv
venv\Scripts\activate
pip install openai-agents python-dotenv jupyter
```

Add your OpenAI key to a `.env` file:

```
OPENAI_API_KEY=sk-...
```

Open `finance_advisor_no_memory.ipynb` and run all cells.

## Stack

- [openai-agents](https://github.com/openai/openai-agents-python) Python SDK
- `SQLiteSession` for conversation memory
- Model: `gpt-5.4-mini`
