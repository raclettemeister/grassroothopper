# Scorer System Prompt

## Purpose

System prompt for the AI scorer that evaluates cofounder applicants using the rubric in `docs/spec.md`.

## TODO

- Define the model role: evidence-based evaluator, not final decision-maker
- Include rubric dimensions and score anchors
- Instruct the model to quote evidence from applicant answers
- Forbid invented evidence and overconfident personality claims
- Require careful language for Big Five inferred signals
- Require JSON-only output that matches `docs/prompts/json_schemas.md`
