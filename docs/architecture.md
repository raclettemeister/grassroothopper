# Grassroot Hopper — Cofounder Headhunter Tool Architecture

*Status: initial draft*  
*Goal: define a no-code-first MVP architecture with a clean upgrade path to a coded system*

---

## 1. Architecture goals

The architecture should do four things well:

1. launch fast with mostly no-code tools
2. keep applicant scoring explainable and auditable
3. protect candidate data and respect GDPR basics
4. leave a clean path toward a stronger coded system later

This is an internal decision-support tool, not a public social product. Simplicity matters more than elegance.

---

## 2. Design principles

- **No-code first.** Do not build custom infrastructure before the funnel proves itself.
- **Structured outputs only.** LLM calls must return JSON that matches an explicit schema.
- **PII minimization.** Only send the minimum needed data into automations and LLM prompts.
- **Human-in-the-loop.** AI suggests; Julien decides.
- **Version everything that matters.** Prompt version, rubric version, scoring run, and timestamps.
- **Replaceable components.** Each MVP tool should map to a future coded equivalent.

---

## 3. Recommended MVP stack

| Layer | MVP choice | Why |
|---|---|---|
| Landing page | Framer, Webflow, or Carrd | fast to publish, good enough for a polished selective landing page |
| Application form | Fillout or Tally | logic, long-form fields, hidden fields, consent, webhook support |
| Automation | Make preferred, Zapier acceptable | better branching, parsing, retries, and multi-step scenarios |
| Database | Airtable preferred; Google Sheets only if absolutely necessary | easy schema, views, interfaces, and lightweight internal dashboard |
| Internal dashboard | Airtable Interface | fastest founder-facing review UI |
| AI scoring | LLM API via HTTP module | structured JSON output with prompt templates |
| Email | Gmail, Resend, or MailerSend | basic confirmation and manual follow-up |
| File storage | links only in MVP; optional Drive folder later | avoid unnecessary uploads at first |

### Recommended exact MVP path

If choosing one stack now:

- **Landing:** Framer
- **Form:** Fillout
- **Automation:** Make
- **Database:** Airtable
- **Scoring:** LLM API with JSON schema prompt
- **Dashboard:** Airtable Interface

That gives the best balance of polish, speed, and control.

---

## 4. MVP system diagram

```text
[Landing Page]
    |
    v
[Application Form]
    |
    v
[Webhook / Form Submission]
    |
    v
[Make Scenario]
    |----> normalize fields
    |----> write Applicants + Responses
    |----> call LLM scorer
    |----> validate JSON
    |----> retry if invalid
    |----> write Scores + recommendation
    |----> send confirmation email
    |----> notify Julien
    v
[Airtable Base]
    |---- Applicants
    |---- Responses
    |---- Scores
    |---- Notes
    |---- RoleTracks
    |---- PromptVersions
    v
[Airtable Interface]
    |
    v
[Julien reviews, adds notes, changes status]
```

---

## 5. Component responsibilities

## 5.1 Landing page

Responsibilities:

- explain project and founder context
- frame the process as cofounder selection, not a job ad
- let candidate choose to start application

Should not:

- store applicant data directly
- expose internal scoring logic in full

## 5.2 Application form

Responsibilities:

- capture role track
- capture narrative answers
- capture self-report items
- capture consent
- send one clean payload downstream

Should include:

- hidden field for campaign/source if needed
- submission timestamp
- version number for question set

## 5.3 Automation layer

Responsibilities:

- normalize incoming form fields
- create or update records
- run scorer
- validate outputs
- handle retries and failure alerts

Should not:

- store secrets in plain text fields
- silently discard malformed scoring output

## 5.4 Database layer

Responsibilities:

- store applicant identity and consent
- store raw responses
- store each scoring run with versioning
- store founder notes and decision states

Should support:

- shortlist view
- confidence filters
- red flag filters
- audit trail of changes

## 5.5 Scoring layer

Responsibilities:

- convert narrative answers into structured rubric outputs
- produce evidence snippets and interview prompts
- state confidence and insufficient-evidence cases clearly

Should not:

- make irreversible decisions
- invent evidence not present in answers

---

## 6. MVP data flow

1. Candidate opens landing page
2. Candidate submits form
3. Form tool sends payload to Make via webhook
4. Make normalizes field names and creates:
   - `Applicants` record
   - `Responses` record
5. Make sends a sanitized scoring payload to the LLM
6. LLM returns structured JSON
7. Make validates required keys and score ranges
8. If invalid:
   - retry once with repair prompt, or
   - mark `score_status = failed_validation`
9. If valid:
   - create `Scores` record
   - update `Applicants.current_score_id`
   - update `Applicants.status = Scored`
10. Send confirmation email to applicant
11. Send internal notification to Julien
12. Julien reviews in Airtable Interface and changes status manually

---

## 7. Data model

The MVP should keep normalized-enough data to survive future migration, while staying simple.

## 7.1 Core tables

### Applicants

One row per person / application attempt.

| Field | Type | Notes |
|---|---|---|
| applicant_id | text / UUID | primary key |
| submitted_at | datetime | source of truth for submission time |
| full_name | text | PII |
| email | email | PII |
| location | text | optional, minimal |
| role_track_id | link | CTO/Builder or Community/Ops |
| source | text | optional source attribution |
| status | single select | New, Scored, Human Reviewed, Shortlist, etc. |
| consent_ai_scoring | checkbox | required |
| consent_privacy | checkbox | required |
| consent_timestamp | datetime | audit trail |
| current_score_id | link | latest successful score run |
| deletion_requested_at | datetime | nullable |
| deleted_at | datetime | nullable |

### Responses

One row per submission payload.

| Field | Type | Notes |
|---|---|---|
| response_id | text / UUID | primary key |
| applicant_id | link | applicant owner |
| question_set_version | text | lets prompts evolve safely |
| raw_answers_json | long text / JSON | original structured form payload |
| proof_links | long text / JSON | GitHub, portfolio, writing, etc. |
| self_report_json | long text / JSON | Big Five style answers |
| submitted_word_count | number | useful for calibration |

### Scores

One row per scoring run.

| Field | Type | Notes |
|---|---|---|
| score_id | text / UUID | primary key |
| applicant_id | link | owner |
| prompt_version_id | link | prompt version used |
| model_name | text | exact provider/model identifier |
| scored_at | datetime | audit |
| composite_score | number | normalized 0-5 |
| confidence_score | number | 0-100 |
| recommendation | single select | shortlist / interview / hold / no-fit-now / insufficient-evidence |
| rubric_scores_json | long text / JSON | per-dimension scores |
| evidence_snippets_json | long text / JSON | quoted support |
| risks_json | long text / JSON | red flags, open questions |
| interview_script_json | long text / JSON | tailored prompts |
| raw_llm_output | long text | raw payload for debugging |
| validation_status | single select | passed / repaired / failed |

### Notes

Human review notes and decision notes.

| Field | Type | Notes |
|---|---|---|
| note_id | text / UUID | primary key |
| applicant_id | link | owner |
| author | text | usually Julien |
| note_type | single select | review / interview / trial / decision |
| body | long text | human notes |
| created_at | datetime | audit |

### RoleTracks

Metadata table for weighting and wording.

| Field | Type | Notes |
|---|---|---|
| role_track_id | text | primary key |
| name | text | CTO / Pragmatic Builder, Community / Ops Architect |
| weighting_json | long text / JSON | role-specific scoring weights |
| active | checkbox | allows future tracks |

### PromptVersions

Track scorer evolution.

| Field | Type | Notes |
|---|---|---|
| prompt_version_id | text | primary key |
| system_prompt_version | text | git-friendly identifier |
| schema_version | text | JSON schema version |
| rubric_version | text | rubric identifier |
| active_from | datetime | audit |

## 7.2 Status model

Recommended applicant statuses:

- New
- Scoring Failed
- Scored
- Human Reviewed
- Shortlist
- Intro Call
- Deep Dive
- Trial
- Offer / Join
- Declined
- Archived
- Deleted

---

## 8. LLM prompting approach

## 8.1 Inputs to the scorer

Send:

- applicant ID
- selected role track
- sanitized question/answer pairs
- self-report summary inputs
- scoring rubric version
- explicit output schema

Do **not** send unless necessary:

- email address
- personal phone
- unrelated notes
- internal founder commentary

## 8.2 Prompt structure

1. **System prompt**
   - describes role: evidence-based evaluator, not judge
   - states scoring dimensions and anchors
   - forbids invented evidence
   - instructs careful language for inferred personality signals
2. **User prompt**
   - includes candidate answers
   - includes role track
   - includes desired JSON schema

## 8.3 Output contract

Require JSON only. Example top-level keys:

- `applicant_id`
- `role_track`
- `scores`
- `composite_score`
- `confidence_score`
- `recommendation`
- `insufficient_evidence`
- `evidence_snippets`
- `big_five_self_report_summary`
- `big_five_inferred_signals`
- `fit_summary`
- `risks`
- `interview_questions`

## 8.4 Validation and retries

Validation steps:

1. JSON parses successfully
2. required keys exist
3. score values are within allowed ranges
4. evidence snippets map to real answers
5. recommendation enum is valid

Retry policy:

- first failure: automatic repair prompt with original output attached
- second failure: mark score run failed and notify Julien

Do not keep infinite retries.

## 8.5 Versioning

Each score run should record:

- model version
- prompt version
- rubric version
- schema version

Without this, calibration becomes guesswork.

---

## 9. Security boundaries

## 9.1 PII storage boundary

PII should live in the database and form provider. The LLM should receive the minimum needed to evaluate the application.

Recommended practice:

- store name and email in `Applicants`
- send only `applicant_id`, role track, and answer text to the LLM
- avoid copying applicant emails into prompt payloads

## 9.2 Secret storage

Store secrets only in:

- Make connection secrets / secret manager
- form provider secret config
- deployment environment variables later

Do not store API keys in:

- Airtable fields
- markdown docs
- prompt files
- email drafts

## 9.3 Access control

MVP access should be minimal:

- Julien: full access
- future reviewer: read-only or limited reviewer permissions
- public: no access to dashboard or raw data

If using Airtable:

- keep base private
- use Interface permissions if collaborators are added later

## 9.4 Logging and audit

Log:

- submission timestamp
- scoring timestamp
- scoring failure reason
- prompt/schema version
- manual status changes
- deletion requests and completion

Do not log secrets.

## 9.5 Backups

At minimum:

- Airtable export or snapshot weekly
- copy prompt and rubric files in git
- export critical applicant data before major schema changes

---

## 10. Rate limits and operational resilience

Potential bottlenecks:

- form provider webhook bursts
- LLM API rate limits
- Make scenario operation caps
- Airtable API limits

MVP mitigation:

- queue submissions through Make scenario one by one
- limit automated retries
- notify Julien on failed scoring runs
- keep a manual rescore button or field trigger

Do not design for thousands of applicants yet.

---

## 11. GDPR and EU / Belgium privacy basics

This is not legal advice, but the MVP should respect the basics from day one.

## 11.1 Lawful basis

Use explicit consent for this selection workflow, especially because AI-assisted scoring is involved and the process is personal.

## 11.2 Data minimization

Collect only what helps answer:

- who is this person
- what role track do they want
- what have they actually done
- can they realistically commit

Avoid collecting:

- unnecessary demographic data
- government IDs
- sensitive personal categories
- irrelevant biographical detail

## 11.3 Transparency

The form should explain:

- why data is collected
- that AI-assisted scoring is used
- that scoring is advisory
- how long data is kept
- how to request deletion

## 11.4 Retention policy

Recommended MVP policy:

- non-shortlisted applicants: keep for **180 days**, then delete
- shortlisted or active conversations: keep for **12 months** from last activity
- deletion requests: process within **30 days**

## 11.5 Consent log

Store:

- consent checkbox state
- consent text version
- timestamp
- form version

## 11.6 Deletion request process

Minimum process:

1. applicant emails the dedicated address
2. Julien marks `deletion_requested_at`
3. relevant records are deleted or anonymized
4. completion timestamp recorded
5. applicant receives confirmation

## 11.7 Processor checklist

For every vendor used, confirm:

- where data is stored
- whether a DPA is available
- whether EU data handling is acceptable
- whether deletion/export is possible

---

## 12. Risks and mitigations

| Risk | Why it matters | Mitigation |
|---|---|---|
| Bias in scoring | strong candidates could be unfairly down-ranked | keep scoring advisory, bias-test examples, avoid demographic collection, review manually |
| Hallucinated evidence | model may invent support for a score | require quote-backed evidence snippets and validation spot checks |
| Prompt injection in answers | candidate may try to manipulate scorer | system prompt must ignore instructions from applicants; treat answers as data only |
| Secrets leakage | automations often spread credentials widely | store secrets only in managed connections and env vars |
| Overconfidence from neat scores | numbers can create fake certainty | always show confidence, evidence, and insufficient-evidence states |
| Tool fragility | no-code tools can silently fail | add failure states, notifications, and manual recovery |
| GDPR failure | personal candidate data is involved | explicit consent, retention rules, deletion workflow |
| Rate limits / cost spikes | repeated scoring can fail or get expensive | throttle runs, version prompts, avoid redundant rescoring |

---

## 13. Testing and calibration

## 13.1 Before launch

- run at least 5 synthetic applicants across obvious strong/mid/weak cases
- verify JSON schema compliance
- verify score ranges and recommendation logic
- verify evidence snippets map to real text
- verify consent fields are stored correctly
- verify deletion workflow manually

## 13.2 Early calibration

After the first 10-20 real applications:

- compare score output against Julien's judgment
- note false positives and false negatives
- tighten or loosen weights only with examples
- review whether Big Five context is helping or distracting

## 13.3 Human override rule

Julien must be able to:

- change status regardless of score
- ignore a recommendation
- request a manual rescore after prompt updates
- annotate why a decision differed from the automated output

---

## 14. Upgrade path to a coded v2

The MVP is intentionally lightweight. If the funnel works, upgrade one boundary at a time.

## 14.1 Mapping from MVP to v2

| MVP component | v2 coded replacement |
|---|---|
| Framer/Webflow/Carrd landing page | Next.js marketing + application app |
| Fillout/Tally form | custom multi-step application flow |
| Make / Zapier automation | queue worker + job runner |
| Airtable | Postgres |
| Airtable Interface | internal admin app |
| LLM call in automation | backend scoring service |
| manual exports | scheduled backups and admin tooling |

## 14.2 v2 architecture diagram

```text
[Next.js Frontend]
    |
    v
[App Backend / API]
    |---- auth for internal reviewers
    |---- application submission API
    |---- deletion request API
    v
[Postgres]
    |---- applicants
    |---- responses
    |---- score_runs
    |---- notes
    |---- audit_logs
    v
[Queue Worker]
    |---- scoring jobs
    |---- retry logic
    |---- email jobs
    v
[LLM Provider]

[Object Storage] for optional attachments
[Monitoring + Logs]
```

## 14.3 What should trigger the upgrade

Move beyond MVP when at least one of these becomes true:

- more than 25-50 serious applications need structured review
- manual error recovery becomes annoying
- multiple reviewers need access
- GDPR and audit pressure increase
- the funnel becomes part of a broader founder/community product stack

---

## 15. Implementation notes

## 15.1 Suggested build order

1. finalize copy and question set
2. create Airtable schema
3. build form
4. build Make scenario
5. add scorer prompt + schema validation
6. build Airtable Interface
7. run synthetic tests

## 15.2 What not to overbuild

- authentication for applicants
- fancy analytics
- attachment uploads
- custom admin UI
- multi-model scoring experiments

---

## 16. Recommended MVP verdict

The right first architecture is:

- polished static landing page
- structured no-code form
- Make automation
- Airtable as operational database and dashboard
- one LLM scoring step with strict JSON validation
- explicit human review and override

That is enough to create a serious inbound pipeline without pretending the infrastructure matters more than the actual candidate signal.
