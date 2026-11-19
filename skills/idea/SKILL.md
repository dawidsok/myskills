---
name: idea
description: Refine a rough seed idea into a challenged draft concept that can later become a PRD. Use when the user invokes /idea, says they have an idea, wants to brainstorm/refine a product concept, or wants a structured interview that combines discovery with Socratic pressure before writing a PRD.
---

# Idea: Refine a Seed Into a Draft Concept

Turn an early idea into a clear, challenged, PRD-ready concept. This skill sits before PRD creation: it is lighter than a full PRD workflow, but more structured and adversarial than open brainstorming.

The output is a **draft concept**, not a PRD. A good draft concept answers: who is this for, what pain does it solve, why now, what is the smallest valuable version, what assumptions could kill it, and what should the PRD explore next?

## Operating stance

Combine three modes:

1. **Facilitator** — draw the user's own thinking out. Do not invent domain facts and present them as truth.
2. **Structured shaper** — move through a deliberate sequence so the idea becomes usable input for a PRD.
3. **Socratic challenger** — pressure-test weak claims, vague users, bloated MVPs, and hidden assumptions.

Be collaborative, direct, and specific. Challenge the idea because it deserves clarity, not because the user needs to be defeated.

## Initial response

When invoked:

1. If the user supplied a seed idea inline, capture it verbatim and begin Step 1.
2. If the user supplied a file path, read it fully, use its contents as the seed idea, and begin Step 1.
3. If no idea was supplied, ask:

```text
I'll help you turn a rough idea into a challenged draft concept that can later become a PRD.

Share the seed idea in messy form:
- What do you want to build?
- Who might it be for?
- What problem, frustration, or opportunity triggered it?

One paragraph is enough. Rough is fine.
```

Then wait.

## Output artifact

By default, write the concept to:

```text
context/foundation/idea-concept.md
```

If `context/foundation/` does not exist, ask whether to create it. If the user says no, keep the concept in the chat and do not write files.

If `context/foundation/idea-concept.md` already exists, ask whether to:

- Resume/refine the existing concept
- Archive it to `context/archive/idea-concept-YYYY-MM-DD-HHMM.md` and start fresh
- Cancel

## Process

Walk one phase at a time. Do not scatter questions across all topics at once. At each phase:

1. Ask one open question.
2. Echo back what you heard in crisp bullets.
3. Identify 2–4 gray areas or decisions.
4. Use `ask_user_question` when structured choices would reduce ambiguity.
5. Challenge vague answers immediately.
6. Lock the phase summary before moving on.

### Step 1: Raw idea capture

Goal: preserve the user's original intent before improving it.

Ask:

```text
In your own words, what is the idea, and what triggered it?
```

Extract:

- Seed idea, quoted or close to the user's wording
- Trigger moment
- Desired change in the world
- Any existing constraints or context

Challenge prompts:

- "What would make this idea not worth building?"
- "What part of this is based on something you've personally observed?"
- "If this is obvious, why doesn't the target user already solve it today?"

### Step 2: User, pain, and stakes

Goal: replace "users" with a specific person in a specific painful moment.

Ask:

```text
Who feels this problem most sharply, when do they feel it, and what does it cost them today?
```

Capture:

- Primary user / persona
- Pain moment
- Current workaround
- Cost of the workaround: time, money, risk, embarrassment, missed opportunity, cognitive load, etc.

If the answer says "everyone", "people", "companies", or "users", push for a narrower first adopter.

Structured gray areas may include:

- First adopter: personal use / individual professionals / teams inside orgs / hobbyist niche
- Pain type: workflow friction / missing capability / decision paralysis / coordination cost / trust or quality problem
- Urgency: daily pain / weekly pain / occasional but expensive / speculative

### Step 3: Promise and wedge

Goal: articulate the product promise and the narrow entry point.

Ask:

```text
What is the smallest promise this idea makes to the primary user?
```

Capture:

- One-sentence concept promise
- Why the user would try it now
- Why existing alternatives are insufficient
- The wedge: the narrow first use case, not the entire future platform

Challenge prompts:

- "What existing tool is closest, and why wouldn't the user just keep using it?"
- "What has to be 10x better, simpler, cheaper, or more timely?"
- "Is this a product, a feature, a workflow, a content business, or an internal tool?"

### Step 4: Smallest valuable concept

Goal: find the first version that proves value without bloating into a full PRD.

Ask:

```text
Walk me through the first successful use from start to value. What does the user do, and what changes for them?
```

Capture the first-use flow as 3–7 steps.

Then force MVP discipline:

- What can be manual behind the scenes?
- What can be hardcoded for the first test?
- What user segment can be excluded?
- What feature is tempting but unnecessary for proof?

Challenge if the flow requires many integrations, multiple user roles, complex automation, marketplace liquidity, or custom infrastructure before any value is visible.

### Step 5: Assumption attack

Goal: expose what must be true for the concept to work.

Create a short assumption map with these categories:

- User assumption — the target user actually has this pain
- Behavior assumption — they will change behavior to use this
- Value assumption — the result is valuable enough to return/pay/share
- Feasibility assumption — the core promise can be delivered acceptably
- Distribution assumption — the user can be reached
- Scope assumption — the small version is enough to learn something real

For each category, ask one hard question. Examples:

- "What evidence would convince you this pain is not real?"
- "What habit or workflow are you asking the user to abandon?"
- "What would the user pay with: money, time, data, trust, attention?"
- "What's the riskiest part technically or operationally?"
- "Where would the first 10 users come from?"

Mark assumptions as:

- Known
- Plausible but unproven
- High-risk unknown

### Step 6: Concept shape decisions

Goal: turn ambiguity into explicit choices.

Use `ask_user_question` for 2–4 decisions that matter most for this idea. Choose from these when relevant:

- Concept type: app / workflow / service / marketplace / content / internal tool
- Primary value: save time / improve decisions / reduce risk / create output / coordinate people / entertain
- First proof: prototype / concierge test / landing page / manual pilot / technical spike
- Business intent: personal tool / open-source project / paid SaaS / agency/service lead-gen / unsure
- PRD readiness: ready for PRD / needs validation / needs narrower scope / park for later

Always include a recommended option when the user's answers make one path clearly safer.

### Step 7: Draft concept write-up

Write `context/foundation/idea-concept.md` using this schema:

```markdown
# Draft Concept: <working title>

## 1. Seed Idea

<original idea in the user's language>

## 2. Primary User and Pain

- Primary user:
- Pain moment:
- Current workaround:
- Cost today:

## 3. Concept Promise

<one-sentence promise>

## 4. Wedge / First Use Case

<narrow initial use case>

## 5. Smallest Valuable Version

1. <first-use step>
2. <first-use step>
3. <first-use step>

## 6. What Is Explicitly Out of Scope

- <non-goal>

## 7. Key Assumptions

| Assumption | Status | How to test |
| --- | --- | --- |
| <assumption> | Known / Plausible / High-risk unknown | <test> |

## 8. Socratic Challenges

- <challenge considered and resolution>

## 9. PRD Readiness

Verdict: Ready for PRD / Needs validation / Needs narrower scope / Park for later

Before PRD, resolve:

- <open question>

Suggested next step:

- <e.g. run a validation interview, build a concierge test, or create a PRD>
```

Do not overfill unknown sections. Use `TBD` or `Open question:` when the user has not provided enough information.

### Step 8: Close

Summarize:

- Working title
- Primary user
- Smallest valuable version
- Riskiest assumption
- PRD readiness verdict
- Path to the written concept

If the concept is PRD-ready, suggest the next skill/command the user normally uses for PRD creation. Do not automatically run it.

## Guardrails

- Do not write a PRD. Write a draft concept.
- Do not pick a tech stack unless the idea itself is specifically about technology choice.
- Do not invent validation evidence. Label guesses as assumptions.
- Do not accept vague target users; narrow to a first adopter.
- Do not let the MVP become the full product vision.
- Do not skip the assumption attack. That is what makes this different from ordinary brainstorming.
- Prefer a smaller, testable concept over a grand but untestable one.
