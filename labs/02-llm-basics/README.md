# Lab 02 — LLM basics on Gemini

## Clone

```bash
git clone https://github.com/Santhosh-Firstlight/agentic-architect-lab.git
cd agentic-architect-lab/labs/02-llm-basics
```

## Set up

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -U google-genai python-dotenv
echo 'GEMINI_API_KEY=your-key-here' > .env    # key from aistudio.google.com
```

## Run the script

```bash
set -a; source .env; set +a
python probe_gemini.py all       # or: basic | turns | models | params
```

## Run the notebook

```bash
pip install jupyterlab
jupyter lab gemini_fundas.ipynb
```

Choose **Kernel → Restart Kernel and Run All Cells**.
