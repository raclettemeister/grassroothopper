# Grassroot Hopper — Cofounder Headhunter Tool Spec

*Status: initial draft*  
*Owner: Julien Thibaut*  
*Purpose: define the MVP product, UX, scoring logic, and operating model for a serious inbound cofounder funnel*

---

## 1. Product in one paragraph

Grassroot Hopper needs a better way to find the right founding teammates than awkward outbound networking, friend-recruiting, or vague "let's grab coffee" conversations. This tool creates an inbound application funnel that feels selective, transparent, and thoughtful. Candidates choose a role track, answer hard questions that reveal how they think and what they have actually done, and receive a clear expectation of next steps. Julien gets a defensible shortlist with explainable reasons, evidence snippets, and interview prompts rather than vibes.

This is not a generic hiring tool. It is for selecting a cofounder or founding team member.

---

## 2. Problem statement

### Current bottleneck

Julien has vision, operator credibility, personal runway, and willingness to lead, but not yet the technical or founding-team counterpart needed to build fast with confidence. The current pattern is familiar and inefficient:

- outbound conversations feel socially awkward
- recruiting friends is safer emotionally, but narrows the pool
- strong strangers do not yet have a serious place to raise their hand
- there is no structured way to compare candidates beyond "good conversation" energy

### Why this product exists

The tool should:

- turn cofounder search into an inbound pipeline
- attract high-agency strangers who like hard, early-stage work
- repel low-fit candidates who need convincing
- demonstrate Grassroot Hopper's own ability to ship useful AI/no-code systems quickly

---

## 3. Goals

### Primary goals

- Convert awkward outbound recruiting into a credible inbound application flow
- Make serious candidates feel this is selective, not casual networking
- Produce explainable shortlist recommendations, not black-box scores
- Surface high-agency, pragmatic, low-ego builders
- Stay shippable by one founder using no-code tools in days or weeks

### Secondary goals

- Show Julien's strengths and limits with unusual honesty
- Generate reusable structured notes for interviews and trial projects
- Create a proof-of-concept for "non-coder founder + AI + no-code can ship fast"

### Success criteria

- Qualified strangers apply without needing personal introduction
- Julien can review applicants in under 15 minutes each after automated scoring
- Shortlist decisions feel evidence-based and readable
- At least one high-fit candidate reaches a meaningful collaboration trial

---

## 4. Non-goals

- Replace human judgment with automated acceptance or rejection
- Diagnose personality or mental health
- Become a general ATS or HR platform
- Optimize for application volume at the expense of signal quality
- Predict long-term cofounder success with certainty
- Collect more personal data than the process truly needs

---

## 5. Product principles

1. **Transparency is a feature.** The landing page should clearly say what Julien brings, what he does not bring, and what kind of partner he actually needs.
2. **Selective by design.** A bit of friction is good. The wrong people should self-select out.
3. **Behavior beats branding.** Concrete examples matter more than polished language.
4. **Advisory, not absolute.** AI scoring helps organize and explain; it does not decide.
5. **Role-track aware.** CTO/Builder and Community/Ops should not be scored as if they were the same role.
6. **No-code first.** The MVP should work with forms, automations, and a lightweight dashboard.
7. **Human override always.** Julien can change status, weights, notes, and shortlist decisions manually.

---

## 6. Users and role tracks

## 6.1 User types

| User | Need | Outcome |
|---|---|---|
| Applicant | Understand what Grassroot Hopper is, whether they fit, and how serious the opportunity is | Submit a thoughtful application or self-select out |
| Julien / founder | Review applicants quickly without reducing everything to vibes | Get ranked applicants, notes, evidence, and interview prompts |

## 6.2 Role tracks

| Role track | Who it is for | What matters most |
|---|---|---|
| **CTO / Pragmatic Builder** | technical cofounder, AI tinkerer, systems thinker, prototype shipper | high agency, execution, ambiguity comfort, technical leverage, communication |
| **Community / Ops Architect** | workshop runner, event/community builder, operator who can mobilize humans | high agency, communication, orchestration, execution, ambiguity comfort |

---

## 7. User journeys

## 7.1 Applicant journey

1. Candidate lands on the page from a link, post, intro, or search result
2. Reads a transparent case for why Grassroot Hopper exists and why Julien is applying pressure now
3. Sees what Julien brings: runway, operator track record, CEO willingness, openness to pivot
4. Sees what Julien lacks: deep technical building ability, need for a pragmatic builder counterpart
5. Selects a role track
6. Completes the application, including concrete examples and consent
7. Sees a serious completion screen with timeline and next steps
8. Receives a confirmation email
9. If shortlisted, enters interview + trial workflow

## 7.2 Founder journey

1. Julien receives a new application record
2. Automation stores raw responses and triggers scoring
3. LLM returns structured JSON with rubric scores, evidence snippets, confidence, red flags, and interview prompts
4. Dashboard shows applicant summary, role track, status, and composite score
5. Julien reads the original answers when needed, adds notes, and changes status
6. Shortlisted applicants move to call, deeper discussion, and a short paid or clearly bounded collaboration test

---

## 8. Core pages

| Page | Purpose | MVP requirements |
|---|---|---|
| **Landing page** | Explain the mission and attract the right people while repelling the wrong ones | founder transparency, role tracks, what Grassroot Hopper is, what stage it is at, why apply now, CTA |
| **Application form** | Capture structured evidence, not just enthusiasm | role track selector, narrative questions, short Big Five self-report, commitment questions, links, consent |
| **Completion page** | Set expectations and reduce ambiguity | timeline, response promise, what review looks like, no-filler tone |
| **Founder dashboard** | Turn submissions into decisions | applicant list, status, scores, confidence, notes, evidence, shortlist filter |

---

## 9. Application flow

## 9.1 Flow steps

1. **Landing**
   - explain the project
   - explain why this is a cofounder search, not job hiring
   - explain what Julien brings and what is still missing
2. **Role track**
   - candidate chooses CTO / Pragmatic Builder or Community / Ops Architect
3. **Basics**
   - name
   - email
   - location / timezone
   - links to relevant work
4. **Fit and evidence questions**
   - long-form answers with word minimums on the most important prompts
5. **Self-report block**
   - lightweight Big Five-style statements for context, not diagnosis
6. **Commitment and constraints**
   - time, financial/risk posture, availability, preferred collaboration mode
7. **Consent**
   - AI-assisted scoring disclosure
   - privacy and deletion rights
8. **Completion**
   - response timeline and what happens next

## 9.2 Intentional friction points

These are features, not bugs:

- application takes roughly 20-30 minutes
- at least 3 questions require concrete examples
- candidates are asked for links, artifacts, or receipts where possible
- one question forces independent judgment, not aspiration talk
- the landing page is honest about uncertainty and early-stage risk

Low-agency people should feel, "this is too much work." Good.

---

## 10. Functional requirements

| ID | Requirement | MVP |
|---|---|---|
| FR1 | Landing page explains project, founder context, role tracks, and seriousness of process | Yes |
| FR2 | Candidate selects one role track | Yes |
| FR3 | Form captures narrative answers with required minimum length on key prompts | Yes |
| FR4 | Form captures optional proof links: GitHub, portfolio, writing, talks, events, prototypes | Yes |
| FR5 | Form captures lightweight Big Five self-report answers | Yes |
| FR6 | Consent must be explicit before submission | Yes |
| FR7 | Submission creates applicant record in database | Yes |
| FR8 | Automation triggers LLM scoring and stores JSON result | Yes |
| FR9 | Founder dashboard shows applicants, scores, confidence, tags, status, and notes | Yes |
| FR10 | Founder can override score-based recommendation manually | Yes |
| FR11 | System generates interview prompts tailored to candidate answers | Yes |
| FR12 | System marks insufficient-evidence cases instead of forcing fake precision | Yes |
| FR13 | Candidate can request deletion of their data | Yes |
| FR14 | Role-track-specific weighting applies in scoring | Yes |
| FR15 | Follow-up task workflow exists | Later |
| FR16 | Applicant portal for status tracking | Later |
| FR17 | Multi-reviewer scoring and calibration views | Later |

---

## 11. Non-functional requirements

| Category | Requirement |
|---|---|
| Speed to build | MVP should be launchable in days or weeks, not months |
| Explainability | Every score must have evidence snippets and human-readable rationale |
| Reliability | Failed scoring runs should retry without losing submissions |
| Privacy | Store only necessary applicant data; provide deletion path |
| Auditability | Keep raw response, score output, timestamp, and model version |
| Maintainability | Prompts, rubrics, schemas, and copy should live in editable markdown files |
| Portability | MVP data structure should map cleanly to Postgres later |
| Bias control | Big Five and inferred signals must be contextual, not deterministic filters |

---

## 12. Question set

## 12.1 Core application questions

| # | Question | Why it exists | Main signals |
|---|---|---|---|
| Q1 | Which role track are you applying for: **CTO / Pragmatic Builder** or **Community / Ops Architect**? | route scoring and follow-ups | role fit |
| Q2 | What about Grassroot Hopper makes you want to apply now, specifically? | distinguish real pull from generic founder curiosity | intrinsic motivation, project understanding |
| Q3 | What is the strongest proof that you ship? Link to something you built, ran, fixed, organized, or launched. What was your actual contribution? | force evidence over self-description | execution, honesty, ownership |
| Q4 | **Tell me about a time a tool/system didn’t do what you wanted, so you bypassed/broke/rebuilt it.** | reveal agency and builder instinct | high agency, technical or operational creativity |
| Q5 | **If we build for 3 months and market ignores it, what do you do Monday morning?** | test reaction to uncertainty and disappointment | ambiguity comfort, problem reframing, execution bias |
| Q6 | **What AI trend is overrated and why?** | test independent thinking and signal-vs-hype judgment | critical thinking, communication |
| Q7 | Tell me about a time you challenged a strong opinion from a founder, lead, or group. What happened? | test healthy disagreeableness without ego theater | communication, low ego, backbone |
| Q8 | Describe a project where the brief was messy or incomplete. How did you create clarity and move it forward? | evaluate action under uncertainty | ambiguity comfort, ownership |
| Q9 | What kind of founder partnership do you work best in, and what kind tends to fail? | test self-awareness and complementarity | collaboration, founder fit |
| Q10 | What level of time and risk can you actually commit in the next 6 months? Be concrete. | avoid fantasy alignment | commitment, honesty |
| Q11 | Tell me about a time you made something simpler instead of more impressive. | reward pragmatism over theater | builder mindset, execution |
| Q12 | What is the most boring repeated task in early-stage company building that you would automate first here, and why? | reveal leverage instincts | systems thinking, prioritization |

## 12.2 Role-track-specific questions

### CTO / Pragmatic Builder track

| # | Question | Main signals |
|---|---|---|
| Q13-B | Show a prototype, script, automation, internal tool, or repo that demonstrates how you work. What trade-off did you make to ship fast? | technical leverage, pragmatism, shipping |
| Q14-B | When have you built with unclear requirements and missing resources, but still produced something useful? | agency, ambiguity comfort, execution |

### Community / Ops Architect track

| # | Question | Main signals |
|---|---|---|
| Q13-C | Tell me about a workshop, event series, community, or operational system you helped run. How did you get people to show up or stay engaged? | orchestration, ownership, social execution |
| Q14-C | Describe a time you created structure for a messy human process. What changed after your intervention? | operational clarity, communication, agency |

## 12.3 Lightweight Big Five self-report block

Use a short, non-clinical 1-5 agreement scale. Label results as **self-report context**, never as diagnosis.

| Trait | Example statements |
|---|---|
| Openness | "I get excited by unfamiliar ideas and experiments." / "I usually look for unusual angles before settling on the obvious path." |
| Conscientiousness | "I reliably close loops without being chased." / "I prefer building repeatable systems over heroic last-minute effort." |
| Extraversion | "I get energy from frequent interaction with people." / "I naturally become visible in group settings." |
| Agreeableness | "I can challenge people directly without making it personal." / "I prefer honest tension over fake harmony when something matters." |
| Emotional stability | "When things are uncertain, I stay functional." / "Setbacks rarely knock me out for long." |

---

## 13. Scoring model

## 13.1 Design principles

- Score observable behavior, not polish
- Quote evidence from the candidate wherever possible
- Treat missing evidence as missing, not bad
- Keep Big Five mostly descriptive, not eliminative
- Make every recommendation reversible by human review

## 13.2 Traits measured

### Core scored dimensions

1. High agency
2. Execution / builder mindset
3. Comfort with ambiguity
4. Communication quality
5. Collaboration style: low ego + useful challenge
6. Founder complementarity
7. Commitment and risk alignment
8. Track-specific capability

### Contextual, lightly weighted or unweighted dimensions

9. Big Five self-report summary
10. Big Five inferred signals from narrative answers

Big Five should shape interview questions, not auto-reject people.

## 13.3 Rubric anchors (0-5)

### High agency

| Score | Observable anchor |
|---|---|
| 0 | No concrete examples; passive language; waits for permission; blames circumstances |
| 1 | Some initiative language, but examples are vague or mostly directed by others |
| 2 | One real example of initiative, but limited ownership or weak outcome |
| 3 | Repeated examples of self-starting within defined scope; takes responsibility and closes loops |
| 4 | Creates options under uncertainty; reframes problems; prototypes or mobilizes resources without waiting |
| 5 | Consistent pattern of self-directed action, leverage creation, and ownership in ambiguous situations; turns blockers into systems or momentum |

### Execution / builder mindset

| Score | Observable anchor |
|---|---|
| 0 | Talks mostly in abstractions; no proof of shipping |
| 1 | Has participated in work, but unclear what they actually delivered |
| 2 | Has shipped small things with help; little evidence of iteration |
| 3 | Can reliably turn ideas into useful outputs; understands trade-offs |
| 4 | Ships quickly, learns from feedback, simplifies aggressively |
| 5 | Repeated pattern of building useful things with speed, clarity, and good trade-offs |

### Comfort with ambiguity

| Score | Observable anchor |
|---|---|
| 0 | Needs certainty, structure, and reassurance before acting |
| 1 | Tolerates ambiguity poorly; examples show stalling or avoidance |
| 2 | Can function in some uncertainty but prefers predefined paths |
| 3 | Can move with incomplete information and create partial clarity |
| 4 | Uses uncertainty well; reframes, tests, and keeps momentum |
| 5 | Thrives in ambiguity without becoming chaotic; creates signal and direction for others |

### Communication quality

| Score | Observable anchor |
|---|---|
| 0 | Evasive, vague, inflated, or hard to follow |
| 1 | Understandable but generic; little precision |
| 2 | Mostly clear, though examples are underdeveloped |
| 3 | Clear, concrete, structured answers with direct language |
| 4 | Precise, thoughtful, concise; handles nuance well |
| 5 | Exceptional clarity with substance, self-awareness, and useful candor |

### Collaboration: low ego + useful challenge

| Score | Observable anchor |
|---|---|
| 0 | Defensiveness, blame, status language, contempt |
| 1 | Either conflict-avoidant or performatively combative |
| 2 | Can collaborate, but evidence of challenge or humility is thin |
| 3 | Can disagree productively and work through tension |
| 4 | Balances backbone and humility; improves outcomes through honest challenge |
| 5 | Strong evidence of principled disagreement, trust-building, and shared ownership |

### Founder complementarity

| Score | Observable anchor |
|---|---|
| 0 | Wants the same role Julien already wants; poor complementarity |
| 1 | Misunderstands the founder gap or wants incompatible working style |
| 2 | Partial fit, but major mismatch on expectations or working model |
| 3 | Reasonable complement to Julien's operator/CEO profile |
| 4 | Strong complement; clearly fills real gaps without power confusion |
| 5 | Exceptional complementarity; sees the partnership shape clearly and constructively |

### Commitment and risk alignment

| Score | Observable anchor |
|---|---|
| 0 | Cannot commit meaningful time or is vague about constraints |
| 1 | Interest is real but timing/risk appetite makes progress unlikely |
| 2 | Possible fit later; current constraints are significant |
| 3 | Realistic, concrete, workable level of commitment |
| 4 | Strong near-term availability and honest risk calibration |
| 5 | Highly aligned commitment with clear readiness for early-stage intensity |

### Track-specific capability

#### CTO / Pragmatic Builder

| Score | Observable anchor |
|---|---|
| 0 | No real technical leverage shown |
| 1 | Technical familiarity, little proof of useful output |
| 2 | Has built things, but unclear depth or practicality |
| 3 | Can build useful MVP systems quickly with pragmatic trade-offs |
| 4 | Strong leverage across prototyping, integrations, automation, and technical judgment |
| 5 | Exceptional practical builder with product sense and fast execution under constraints |

#### Community / Ops Architect

| Score | Observable anchor |
|---|---|
| 0 | No real orchestration evidence |
| 1 | Participated in communities or events, but no ownership signal |
| 2 | Some organizing ability; weak proof of repeatable outcomes |
| 3 | Can run people/process/event systems reliably |
| 4 | Strong evidence of mobilizing communities, creating structure, and keeping momentum |
| 5 | Exceptional human systems builder; repeatedly turns loose groups into functioning engines |

## 13.4 Weighting by role track

### CTO / Pragmatic Builder weighting

| Dimension | Weight |
|---|---|
| High agency | 25% |
| Execution / builder mindset | 20% |
| Comfort with ambiguity | 15% |
| Track-specific capability | 15% |
| Communication quality | 10% |
| Collaboration: low ego + useful challenge | 10% |
| Commitment and risk alignment | 5% |
| Founder complementarity | advisory, shown separately |
| Big Five self-report + inferred signals | context only |

### Community / Ops Architect weighting

| Dimension | Weight |
|---|---|
| High agency | 20% |
| Track-specific capability | 20% |
| Communication quality | 15% |
| Execution / builder mindset | 15% |
| Comfort with ambiguity | 10% |
| Collaboration: low ego + useful challenge | 10% |
| Commitment and risk alignment | 5% |
| Founder complementarity | 5% |
| Big Five self-report + inferred signals | context only |

## 13.5 Confidence score and insufficient evidence

The system should produce both a **composite fit score** and a **confidence score**.

### Confidence inputs

- answer completeness
- specificity of examples
- presence of evidence links or receipts
- directness of response to the actual question
- internal consistency across answers

### Confidence output

| Confidence | Meaning |
|---|---|
| 80-100 | strong evidence base |
| 60-79 | usable, but human review should verify weak spots |
| 40-59 | thin evidence; do not auto-shortlist |
| below 40 | insufficient evidence |

### Insufficient-evidence rule

If fewer than 4 core dimensions have strong direct evidence, mark the application:

> **Insufficient evidence for confident recommendation**

The system should still summarize the candidate, but must not force an artificially precise recommendation.

## 13.6 Thresholds and recommendation bands

| Band | Rule |
|---|---|
| Strong shortlist | composite >= 4.0/5, confidence >= 70, no hard red flags |
| Interview-worthy | composite 3.4-3.9, confidence >= 60 |
| Hold / revisit | composite 2.8-3.3 or confidence below threshold |
| Not a fit now | composite < 2.8 or hard red flag |

## 13.7 Red flags

### Hard red flags

- title/status motivation more prominent than mission or work
- cannot state realistic time commitment
- openly needs convincing to care
- disrespectful, manipulative, or contemptuous tone
- idea-only positioning with no real execution evidence
- obvious mismatch on risk, ethics, or founder expectations

### Soft red flags

- strong claims with no receipts
- over-attachment to one fixed product idea
- inability to explain trade-offs
- high self-rating with weak examples

## 13.8 Anti-gaming measures

- require concrete examples, not just opinions
- ask for links to work where possible
- compare self-report with behavior-based answers
- keep at least one question unpredictable and judgment-heavy
- use confidence penalties when answers are polished but empty
- optionally issue a short follow-up task before final decision

---

## 14. Outputs

Each applicant record should produce:

1. **Applicant summary**
2. **Role track**
3. **Composite fit score**
4. **Confidence score**
5. **High agency score with evidence snippets**
6. **Big Five self-report summary**
7. **Big Five inferred signals** with careful language
8. **Fit summary:** "Why this person might work with Julien"
9. **Risks / open questions**
10. **Suggested interview questions**
11. **Recommended next step**: shortlist, hold, or no-fit-now

### Output language rules

- avoid deterministic psychological language
- avoid pseudo-clinical certainty
- quote the candidate directly where possible
- distinguish observation from interpretation

---

## 15. Candidate experience

## 15.1 What happens after applying

- immediate confirmation page
- confirmation email within minutes
- review within 7 calendar days in normal conditions
- shortlisted people receive a clear note and next-step invite
- no-fit-now candidates may receive a respectful short decline later, but MVP can start with manual follow-up only

## 15.2 Desired tone

- serious
- warm
- direct
- not performatively "startup"
- transparent about uncertainty

---

## 16. Founder admin workflow

1. **New**
2. **Scored**
3. **Human reviewed**
4. **Shortlist**
5. **Intro call**
6. **Deep dive / working session**
7. **Trial project or bounded collaboration**
8. **Decision**
9. **Archived / declined**

### Review checklist

- Read score summary first
- Read raw answers for any candidate above threshold or with unusual signal
- Confirm high-agency evidence is real
- Check mismatch between self-report and behavior-based answers
- Add manual notes before changing status

### Trial project guidance

For serious candidates, use a short, bounded, real piece of work:

- CTO track: prototype, automation, technical teardown, or architecture exercise
- Community/Ops track: event system design, outreach plan, workshop flow, or operating cadence proposal

If the work is non-trivial, pay for it.

---

## 17. MVP scope

## 17.1 Week 1 deliverables

- [ ] landing page copy drafted and published
- [ ] application form live with role tracks and consent
- [ ] Airtable or equivalent base created
- [ ] automation flow from form to database to scorer
- [ ] scorer prompt and JSON schema drafted
- [ ] founder dashboard with shortlist/status views
- [ ] 5 synthetic test applicants run through the flow
- [ ] 1-3 real friendly testers complete the form and give feedback

## 17.2 Postpone until later

- custom web app
- applicant login portal
- advanced analytics dashboard
- multi-rater review workflow
- PDF report generation
- automated decline emails
- psychometric calibration beyond lightweight context scoring
- a public "talent network" or marketplace layer

---

## 18. Metrics

| Metric | Why it matters |
|---|---|
| Landing page visit -> application start rate | checks whether the pitch attracts the right people |
| Application completion rate | tells whether friction is filtering or just breaking UX |
| Qualified applicant rate | measures funnel quality |
| Shortlist rate | reveals scoring strictness and source quality |
| First interview rate | shows whether shortlisted people stay engaged |
| Trial-project conversion | stronger signal of actual founder-fit momentum |
| Time to first high-fit candidate | direct recruiting outcome |
| Time-to-review per applicant | operational efficiency |
| False positive / false negative notes | calibration learning over time |

---

## 19. Sample copy blocks

## 19.1 Landing page sample

> Grassroot Hopper is early. There is no polished company machine here yet. What there is: a founder with runway, operator experience, and the willingness to be CEO for real. What is missing is the right builder or founding operator who likes ambiguity, hates bullshit, and wants to help shape something from the beginning.
>
> If you need certainty, this is not for you. If you create options, ship fast, and want to build something human-sized and meaningful, apply.

## 19.2 Consent copy sample

> I understand my application will be reviewed with AI-assisted scoring to help structure notes, surface patterns, and suggest interview questions. I understand this scoring is advisory and does not make final decisions. I consent to Grassroot Hopper storing my responses for the purpose of this cofounder selection process, and I understand I can request deletion of my data.

## 19.3 Confirmation email sample

**Subject:** Grassroot Hopper application received

> Thanks for applying.
>
> This is a real review process, not a vanity form. I will read strong applications carefully and aim to reply within 7 days.
>
> If you are shortlisted, the next step will likely be a direct conversation and then a small, real piece of collaborative work.
>
> — Julien

---

## 20. Open questions

- Should the MVP include a required mini-task up front, or only after shortlist?
- How much Big Five context is useful before it becomes fake precision?
- Should the landing page mention Julien's available cash runway explicitly or only qualitatively?
- Should decline emails be manual at first to preserve tone?
- What is the minimum evidence threshold for people without public proof links?

---

## 21. MVP summary

Build the smallest serious thing:

- one landing page
- one application form
- one scoring automation
- one founder dashboard
- one human making final decisions

If this works, it creates more than applicants. It creates signal: Grassroot Hopper can ship.
