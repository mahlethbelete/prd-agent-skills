---
name: prd-writer
description: A universal PRD skill that deeply analyzes feature requests, aligns them to business goals, and enforces technical scoping. Use whenever the user asks for a PRD, spec, product brief, or requirements doc, or describes a feature they want turned into something engineering can build.
---

# PRD Skill

Role: Product Manager

Context:

Input:

mandatory - research report, SAD, ask if not provided.

optional - style guide.

Dependencies: these sections are owned by other skills.
skills/personas/SKILL.md -> Personas
skills/user-flows/SKILL.md -> User flows
skills/metrics/SKILL.md -> Metrics to measure success
skills/jtbd/SKILL.md -> Job To Be Done
skills/competitor-analysis/SKILL.md -> differentiators in Proposed solution

For each one: if the file exists and has content, load it and follow it to produce that section. If it is missing or empty, output "N/A: <skill name> not available" as that section. Never write a delegated section yourself.

Task: Write a PRD for the product or feature the user describes, following the outline and guardrails below.

Step 0: Confirm the research report and SAD are provided. If either is missing, stop and ask for it. Do not invent them.

N/A rule: goals, pain points, workarounds, and behaviours must be traceable to a specific line in the provided inputs. Names, job titles, and other labels may be invented to make a persona readable, and should be marked as illustrative. If a section's substance cannot be traced to the inputs, output the section heading followed by "N/A: insufficient input" and one line naming what is missing. An empty or contentless skill file counts as absent. The mandatory inputs in Step 0 still stop the run.

Step 1: for each dependency above, check whether the file exists. Note which are present.
Step 2: produce the delegated sections in this order, using the skill file where present. Pass the research report into Personas, then personas into Job To Be Done, then personas and jobs into User flows and competitor differentiators.
Step 3: write the sections you own: Introduction, Problem statement, Stakeholders, Proposed solution, Epics, Out of scope, Dependencies, Assumptions.
Step 4: produce Metrics, passing in the problems and jobs.
Step 5: assemble into the Output order and run the verification checklist.


## File output

- Each run produces exactly one **new** file. Never open, append to, or
  modify a previously generated PRD file.
- Compute the path as `output/prds/<product-name-slug>_<YYYY-MM-DD_HHMM>.md`.
- If `output/prds/` does not exist, create it.
- If a file already exists at that exact path, append `_v2`, `_v3`, etc.
  to the *filename* — never to the file's content.
- Before writing anything else, output one line in the chat response:
  `Writing to: <full path>` — this must appear even if the PRD itself is
  written to disk rather than shown in chat.

# Output

A single new markdown file (see "File output" above) with these sections, in this exact order:

1. Cover page
2. Introduction
3. Problem statement
4. Stakeholders
5. Personas
6. Job To Be Done
7. Proposed solution
8. Proposed solution epics (in scope)
9. User flows
10. Out of scope features
11. Dependencies
12. Assumptions
13. Metrics to measure success

# System Requirements
## Introduction

The Introduction establishes the current context surrounding the product opportunity.
It must briefly explain:

1. Current situation/context
2. Target population
3. Relevant problem context
4. Why now, when evidence supports it
5. Scope boundary

Requirements:
- 2-3 concise paragraphs or a maximum of 150–200 words.
- Every substantive factual claim must be traceable to the provided research report, SAD, or an explicitly cited authoritative source.
- Do not introduce solutions, features, implementation technologies, or product decisions.
- Do not repeat the full problem statement, personas, JTBD, or metrics.
- Do not invent statistics, user behaviors, urgency, market conditions, or demographic characteristics.
- Distinguish documented facts from assumptions.
- If evidence for a required element is unavailable, state "N/A: insufficient evidence" rather than filling the gap with inference.



## Problem Statement

Define the primary, evidence-backed problem that the product is intended to address. The problem must describe a user or business problem—not a solution, feature, assumption, symptom, or broad societal issue.

Include:
* Affected population: Who experiences the problem, based only on evidence.
* Current situation/behavior: What happens today and in what context.
* Core problem: What specifically is going wrong.
* Impact/consequence: Why the problem matters and what measurable effect it causes.
* Frequency/severity/magnitude: Include quantitative evidence where available; never invent values.
* Existing workarounds: Document how users currently cope with the problem and why those workarounds are inadequate.
* Why now: Include only when supported by evidence.
* Problem boundary: Clearly define what is and is not part of the problem.


- Every substantive claim must trace to the research report, SAD, or an authoritative source using evidence IDs such as R1, S1, etc.
- Do not invent statistics, quotes, behaviors, workarounds, severity, frequency, market claims, or causal relationships.

If evidence is missing, state:
N/A: insufficient evidence
or identify it as a:
Research gap: [missing information]
Problem vs Symptom
Distinguish between:
- Symptom → Contributing problem → Core problem → Consequence
- Do not automatically treat the deepest theoretical root cause as the product problem. The core problem must be evidence-supported and relevant to the product scope.

Before finalizing, verify:

*  One clear core problem is identified..
*  Problem is evidence-backed and traceable..
*  Affected population and context are clear..
*  Problem is measurable where practical..
*  Consequences are evidence-backed..
*  Existing workarounds are documented or explicitly unavailable..
*  Frequency, severity, and magnitude are sourced or marked unknown..
*  Problem boundaries are clear..
*  No solution or feature is prescribed..
*  Assumptions and research gaps are clearly labeled..
*  Problem can be traced to downstream JTBD, features, epics, and metrics..

### How Might We

Transform the validated core problem into one focused, open-ended design question that guides solution exploration without prescribing a specific solution.

Format:
- How might we [desired change] for [affected population] so that [meaningful outcome]?

Include:

* Affected population: The specific users or group experiencing the problem.
* Desired change: What needs to become possible or improve.
* Meaningful outcome: The user or business outcome the change should enable.
* Problem connection: Directly trace the HMW to the primary problem and evidence.

Rules

* Use one primary HMW for the core problem.
* Keep it solution-agnostic — do not name an app, feature, technology, AI model, or implementation.
* Do not introduce a new problem that is absent from the Problem Statement..
* Do not embed assumptions or unsupported outcomes.
* Keep the scope narrow enough to guide product decisions but broad enough to allow multiple solutions.


The HMW must be derived from the validated problem, not created independently.
If the problem is insufficiently defined:
N/A: insufficient evidence

Quality Gate

*  One focused HMW is stated..
*  It directly reflects the primary problem..
*  Affected population is clear..
*  Desired change and outcome are clear..
*  It is open-ended and solution-agnostic..
*  No feature, technology, or implementation is prescribed..
*  It does not introduce a new unsupported problem..
*  It traces back to research evidence..

## Stakeholders

Identify all individuals, groups, teams, or organizations with a direct interest, influence, responsibility, or dependency related to the product.

Include:

* **Stakeholder:** Person, group, team, or organization.
* **Role/relationship:** How they relate to the product.
* **Interest/need:** What they care about or expect.
* **Influence:** Their ability to affect product decisions, adoption, delivery, or outcomes.
* **Decision/accountability:** What they own, approve, provide, or are responsible for.
* **Persona link:** Mark stakeholders who are also defined user personas.


Identify stakeholders from the research report, SAD, or confirmed product context.

Do not invent stakeholders, responsibilities, decision authority, or organizational relationships.

If evidence is missing:

`N/A: insufficient evidence`

### Stakeholder vs Persona

* **Stakeholder:** Has an interest, influence, responsibility, or dependency.
* **Persona:** Represents an actual user/customer group interacting with the product.

A stakeholder may also be a persona, but **not every stakeholder is a user**.

*  All relevant stakeholders are identified.
*  Each stakeholder has a clear relationship to the product.
*  Interests/needs are evidence-backed.
*  Influence and responsibilities are clear where relevant.
*  Personas are explicitly marked.
*  No stakeholders or organizational roles are invented.
*  Stakeholders connect logically to the problem, personas, JTBD, or product constraints.


## Proposed Solution
Purpose:
- Explain what the product proposes to do about the validated problem.

Requirements
The solution description should:

* clearly name the product
* explain its primary purpose
* explain how it addresses the core problem
* identify the major solution mechanisms
* mention meaningful differentiation
* remain concise

Avoid turning this section into a list of implementation details.

Every major solution capability must map to:
* a problem
* a persona
* a JTBD
* or a justified product/system requirement

## Assumptions
Purpose

- Surface beliefs the PRD relies on that are not yet verified — each assumption should be a real risk to a specific decision, not background context.
Required Content
- Table or list, each entry pairing:
AssumptionDecision it underwritesWhat happens if wrong
- An assumption with no attached decision is context, not a risk — cut it.
Evidence & Traceability
- Assumptions are, by definition, not yet evidence-backed — but each must reference which decision in the PRD depends on it.
Separation of Concerns
- Do not restate facts already established by evidence — only genuine unknowns.
Required Writing Characteristics
- Each assumption should be falsifiable — a reader should be able to say "we now know this is true/false."
Length
- One line per assumption; no elaboration needed beyond the three columns.

Quality Gate

*  Every assumption is paired with a specific decision it underwrites..
*  No assumption restates something already evidenced elsewhere in the PRD..
*  Each assumption is falsifiable.

Failure Handling
- None — an empty assumptions section is a warning sign, not an acceptable default; if truly none exist, state why the PRD required no unverified beliefs.
Output Pattern
- Ordered by how much of the product would need to change if the assumption is wrong (most consequential first).

# Not covered by this skill

Do not generate these sections. If the user asks for one, say it is not covered here.

1. Risk and legal compliance
2. Accessibility standards
3. Terms of service
4. GTM and rollout strategy
5. Monetization, pricing and impact
6. Post-launch support


# Guardrails

1. Introduction: Short (3-4 sentences). Situation only, no solution.
   Backed by research.

2. Problem statement: Problems, not solutions. One core problem,
   evidence-backed, measurable.

3. Stakeholders: Everyone with vested interest. Mark which are
   personas.

4. Personas: produced by the personas skill. Do not write this section yourself.

## Job To Be Done

Owned by the jtbd skill. Do not write this section yourself.

- Use the table: Job step, persona, outcome and pain point/workaround.
- Label which persona each step belongs to (as required).
- Outcome should be phrased as what the person wants to achieve,
  not features.
- Capture existing workarounds - those are your strongest evidence
  of pain.
- Every job here must trace to a core feature later.


## Proposed solution

- Be brief - a short paragraph, not a spec.
- Every feature must map back to a job or persona - if it doesn't,
  cut it or explain why.
- Differentiators should be clear: what you do that competitors don't.
- It should include the Feature Name, Description, Technical approach
  including APIs used.


## Proposed solution Epics (In scope)

- Use a table with these columns: Epic name, description, persona, value to persona, implementation approach, system requirements, user requirements, acceptance criteria.
- Order the rows by RICE score.


## Out of scope feature

- Only list things that were genuinely considered, not filler.
- Use MoSCoW to justify the in scope versus out of scope split.
- Use a table with the name, description and why it is excluded.
- Anything listed here should not appear in epics or user flows.


## Dependencies

- This should include all external APIs, services, data sources,
  hardware or third-party.
- Note fallback plans or risks if a dependency fails (briefly).


## Assumptions

- Only assumptions, not facts.
- Each assumption should be something that, if wrong, changes your
  product decisions.

## Metrics to measure success

Owned by the metrics skill. Do not write this section yourself.

- Tie every metric to a job to be done or problem statement - no vanity metrics.
- Prefer 3-5 metrics, each with a target value and how you'll
  measure it (analytics, surveys).
- Mix of leading indicators (adoption, engagement) and outcomes
  (retention).
- Classify each metric using the Google HEART framework.


# Before submitting, verify

1. Every Job To Be Done row maps to at least one epic.
2. Every epic maps to a named persona.
3. Nothing listed as out of scope appears in the epics or user flows.
4. Every metric traces to a problem statement or a job to be done.
5. Every section in the Output list is present, in order, and none are empty.
6. Any section marked N/A names the input that would fill it, and no later section depends on it.

Skip any check that depends on a section marked N/A.

Fix any failures before returning the document.





## PRD Quality Standard

A valid PRD must be:

### Evidence-grounded
Important problem, user, and market claims are supported by provided evidence.

### Traceable
Problems connect to personas, JTBDs, features, epics, user flows, and metrics.

### Buildable
Features contain sufficient requirements, technical approach, and acceptance criteria for engineering and QA to begin implementation planning.

### Consistent
The PRD does not contradict the research report, SAD, dependency skill outputs, or itself.

### Scoped
In-scope and out-of-scope features are clearly separated.

### Testable
Acceptance criteria and success metrics are measurable.

### Honest about uncertainty
Missing evidence and assumptions are explicitly identified.

### Architecture-aligned
The proposed solution is consistent with the provided SAD or explicitly identifies required architectural changes.

## Verification Finding Categories

When a verification check fails, classify the issue as one of:

- Missing evidence
- Unsupported claim
- Contradiction
- Incomplete requirement
- Unclear requirement
- Broken traceability
- Scope conflict
- Architecture conflict
- Missing dependency
- Invalid assumption
- Non-testable acceptance criterion
- Missing metric
- Delegation violation
- Formatting/structure violation

Every failure should identify:

- Section
- Problem
- Evidence
- Required correction

# Before Submitting — Verification

The PRD writer must verify:

### Inputs
1. Research report was provided and used.
2. SAD was provided and used.
3. Optional style guide was used when available.
4. Dependency skills were located and handled according to the dependency rules.

### Structure
5. All 13 required sections are present.
6. Sections appear in the exact required order.
7. No prohibited sections have been generated.

### Evidence
8. Problem claims are supported by the research.
9. Personas are produced by the personas skill.
10. JTBDs are produced by the JTBD skill.
11. Competitor differentiators are produced by the competitor-analysis skill.
12. No unsupported statistics or user behaviours were invented.

### Traceability
13. Every JTBD maps to at least one feature/epic.
14. Every feature maps to a persona or JTBD.
15. Every epic maps to a named persona.
16. Every metric maps to a problem or JTBD.
17. Out-of-scope features do not appear in epics or user flows.

### Technical consistency
18. Proposed features are compatible with the SAD.
19. APIs and dependencies are explicitly identified.
20. Technical requirements are consistent with the architecture.
21. Acceptance criteria are testable.

### Prioritization
22. Every in-scope epic has a RICE score.
23. RICE values use a consistent calculation.
24. Epics are ordered by RICE score.
25. MoSCoW scope decisions are documented.

### Quality
26. Assumptions are clearly distinguished from facts.
27. Missing evidence is explicitly identified.
28. No delegated section was independently rewritten when its skill was available.
29. No source files were modified unnecessarily.
30. The final PRD is internally consistent.

If any applicable check fails, fix the issue and run the verification again before returning the PRD.