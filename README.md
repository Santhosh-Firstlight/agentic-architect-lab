# Agentic Architect Lab

Hands-on portfolio of an OTT / platform architect (16+ years, AWS Solutions Architect Professional, Google Professional Cloud Architect) building production-minded agentic AI systems across AWS, Azure and Google Cloud.

Every lab is runnable, every number in a results file came from a real run, and every design choice of consequence has an ADR.

## Repository layout

| Path | What lives there |
|---|---|
| [`projects/`](projects/) | Portfolio builds: end-to-end agentic systems with architecture, IaC, evals, cost and security notes |
| [`labs/`](labs/) | Short, focused learning labs (one concept each), with measured results |
| [`docs/adr/`](docs/adr/) | Architecture Decision Records that apply across labs and projects |
| [`notes/`](notes/) | Weekly learning notes in my own words |

## Projects

| # | Project | Platform | Status |
|---|---|---|---|
| 1 | Agentic workflow on AWS (Bedrock, AgentCore) | AWS | Planned |
| 2 | Multi-agent system with A2A (Foundry Agent Service) | Azure | Planned |
| 3 | ADK agent on Agent Runtime | Google Cloud | Planned |

## Labs

| Lab | Topic | Stack | Key finding |
|---|---|---|---|
| [02-llm-basics](labs/02-llm-basics/) | Tokens, context, sampling, system instructions, thinking budget | Gemini Interactions API | Client-side history grew input 17 → 761 tokens by turn 3; thinking tokens can consume the whole output cap |

## Conventions

- One folder per lab: `README.md` (how to run), `results.md` (what I measured), code, `requirements.txt`.
- Secrets only in `.env` (git-ignored); copy `.env.example` to start.
- Model IDs are pinned in code and recorded in each results file with the run date.
