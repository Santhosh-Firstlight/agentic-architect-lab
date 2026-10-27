# Projects

Each project is a self-contained, deployable system:

```
projects/<nn-name>/
  README.md          problem, architecture diagram, how to run, demo
  docs/adr/          decisions specific to this project
  src/               application and agent code
  infra/             IaC (CDK / Terraform / Bicep)
  evals/             test sets and evaluation results
  COST.md            cost model and measured spend
  SECURITY.md        threat model (OWASP LLM / agentic risks), guardrails
```
