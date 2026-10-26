# Lab 02 — LLM basics on Gemini

This lab repeats the four basics from Anthropic's `anthropic_api_fundamentals` notebooks 01–04 on the Gemini **Interactions API** (`google-genai` SDK):

1. A first call and its token usage
2. Multi-turn conversations: client-side history, no history, and server-side state
3. A comparison of two models
4. Generation parameters: `max_output_tokens`, `stop_sequences`, `temperature`, `system_instruction` and `thinking_level`

| File | What it is |
|---|---|
| `probe_gemini.py` | Command-line script. Runs any section on its own. |
| `gemini_fundas.ipynb` | The same experiments as a Jupyter notebook |
| `results.md` | The numbers and findings from one run |

Models used:

| Constant | Model | Notes |
|---|---|---|
| `CHEAP` | `gemini-3.5-flash-lite` | Stable. Default `thinking_level=minimal`. |
| `SMART` | `gemini-3.8-flash` | Stable. Newest Flash. Uses thinking tokens by default. |

## Run it locally

### 1. Set up

Get an API key at [aistudio.google.com](https://aistudio.google.com/apikey), then run:

```bash
cd labs/02-llm-basics
python3 -m venv .venv && source .venv/bin/activate
pip install -U google-genai python-dotenv   # tested with google-genai 2.33.0, Python 3.14
```

Put the key in a `.env` file in this folder. The repo's `.gitignore` excludes `.env`, so it stays out of git:

```bash
echo 'GEMINI_API_KEY=your-key-here' > .env
```

### 2a. Run the script, one section at a time

The script reads the key from the environment, not from `.env`, so load `.env` into your shell first. Then save each section's output with `tee`:

```bash
set -a; source .env; set +a

python probe_gemini.py basic  | tee run-output.md
python probe_gemini.py turns  | tee -a run-output.md
python probe_gemini.py models | tee -a run-output.md
python probe_gemini.py params | tee -a run-output.md
```

To run every section in one go, use `python probe_gemini.py all`. Use a different file name from `results.md` so the recorded findings aren't overwritten.

### 2b. Or run the notebook

```bash
pip install jupyterlab
jupyter lab gemini_fundas.ipynb
```

Choose **Kernel → Restart Kernel and Run All Cells**. The notebook loads `.env` itself.

## What to look for in each section

| Section | What to check |
|---|---|
| `basic` | A haiku, then a line like `status=completed in=… out=… thought=… latency=…` |
| `turns` | **A** (you resend the whole history): input tokens grow every turn. **B** (no history): the model doesn't know your name. **C** (`previous_interaction_id`, the server keeps the history): the model remembers you. Compare its input tokens with A's. |
| `models` | Latency and tokens for Flash-Lite compared with 3.8 Flash, including 3.8 Flash's thinking tokens |
| `params` | `max_output_tokens=10` should end `incomplete`, and 3.8 Flash may return no text because thinking uses up the cap. The stop sequence `}` cuts the JSON off just before the closing brace. Temperature 0 and 1 should show the same variety, because the setting is ignored. The French tutor test shows whether the system instruction holds against an override attempt. `thinking_level` minimal vs high shows how thought tokens and latency change. |

Write your numbers in `results.md`. One recorded run is already there.

## Common errors

| Error | Cause and fix |
|---|---|
| `401` / `API key not valid` | `GEMINI_API_KEY` isn't set in the current shell. Run `set -a; source .env; set +a` again. |
| `AssertionError: GEMINI_API_KEY not set` (notebook) | `.env` is missing or isn't in the same folder as the notebook. |
| `404` model not found | The model was renamed or retired. Pick a current ID from [ai.google.dev/models](https://ai.google.dev/models) and update `CHEAP` and `SMART`. |
| `400` invalid argument on `thinking_level` | That model doesn't support the level. For example, 3.8 Flash supports `low`, `medium` and `high`, but not `minimal`. |
| `429` | You've hit a rate limit (the free tier is the tightest). Run one section at a time or increase the `time.sleep`. |
| `ModuleNotFoundError: google` | The venv isn't active, or the notebook kernel isn't using `.venv`. |

## Cost

A full run is a few dozen short calls, so expect a few cents at most. Check your quota in AI Studio. There's nothing to tear down.
