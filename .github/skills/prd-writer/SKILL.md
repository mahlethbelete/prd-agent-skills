---
name: prd-writer
description: A universal PRD skill that deeply analyzes feature requests, aligns them to business goals, and enforces technical scoping. Use whenever the user asks for a PRD, spec, product brief, or requirements doc, or describes a feature they want turned into something engineering can build.
---

# PRD Skill

Role: Product Manager

## Purpose

Produce a product requirement document that an engineering team can build from, based only on the evidence the user provides.

The skill assembles the document. It writes the sections it owns and delegates the rest to separate skills. Where a delegated skill or its inputs are unavailable, the section is marked N/A rather than invented.

The process is:

> **Inputs to Evidence to Draft to Verify to Assemble**

not:

> **Assume to Infer to Fill the gap**

## When to Use

Use this skill when the user:

- Asks for a PRD, spec, product brief, or requirements document
- Wants existing research turned into a scoped deliverable

Do not use it to:

- Invent research, users, or requirements the inputs do not contain
- Produce a go to market plan, pricing model, or compliance review
- Redesign the architecture or select technologies
- Write a section that belongs to a delegated skill

## Inputs

mandatory

- Research report: source for the problem statement, stakeholders, and evidence behind every claim
- System architecture diagram (SAD): source for the technical approach and dependencies

Ask for either if it is not provided. Do not invent them.

**Optional**

- Style guide: applies to tone and formatting only

## Dependencies

These sections are owned by other skills:

| Skill file                            | Section it produces                      |
| ------------------------------------- | ---------------------------------------- |
| `skills/personas/SKILL.md`            | Personas                                 |
| `skills/jtbd/SKILL.md`                | Job To Be Done                           |
| `skills/user-flows/SKILL.md`          | User flows                               |
| `skills/metrics/SKILL.md`             | Metrics to measure success               |
| `skills/competitor-analysis/SKILL.md` | Differentiators within Proposed solution |

For each one: if the file exists and has content, load it and follow it to produce that section. If it is missing or empty, output `N/A: <skill name> not available` as that section. Never write a delegated section yourself.

Task: Write a PRD for the product or feature the user describes, following the outline and guardrails below.

## Evidence Rules

Every statement in the PRD must rest on something the user provided.

**Traceable**

- Goals, pain points, workarounds and behaviours must trace to a specific line in the inputs.
  **Permitted**

- Names, job titles and other labels may be invented so a persona reads naturally. Mark these as illustrative.
  **Not permitted**

- Filling a gap with a plausible answer
- Treating a stakeholder list as user research
- Presenting planned functionality as implemented
- Carrying content forward from a previous run
  Where a section's substance cannot be traced to the inputs, output the section heading followed by `N/A: insufficient input` and one line naming what is missing. An empty or contentless skill file counts as absent.

## Process

**Step 1. Confirm inputs.** Check the research report and SAD are present. If either is missing, stop and ask for it.

**Step 2. Check dependencies.** For each skill in the dependency table, note whether the file exists and has content.

**Step 3. Produce delegated sections.** In order: Personas, then Job To Be Done, then User flows and competitor differentiators. Pass the research report into Personas, personas into Job To Be Done, and personas plus jobs into User flows.

**Step 4. Write owned sections.** Introduction, Problem statement, Stakeholders, Proposed solution, Epics, Out of scope, Dependencies, Assumptions.

**Step 5. Produce Metrics,** passing in the problems and jobs.

**Step 6. Assemble and verify.** Order the sections as below and run the verification checklist.

Output: a single markdown file with these sections, in this exact order:

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

Formatting:

- Use a table for core features, JTBD, in and out of scope features and metrics.
- Use a flow chart for the SAD. If the SAD is provided as an image or a format you cannot read as text, embed or reference it as given. Do not redraw it. Insert the user flows exactly as the user flow skill returns them.
- Create a cover page with product name, date & time.

## Section Requirements

## Introduction

The Introduction establishes the current context surrounding the product opportunity.
It must briefly explain:

1. Current situation/context
2. Target population
3. Relevant problem context
4. Why now, when evidence supports it
5. Scope boundary

Requirements:

- 3–5 concise paragraphs or a maximum of 150–200 words.
- Every substantive factual claim must be traceable to the provided research report, SAD, or an explicitly cited authoritative source.
- Do not introduce solutions, features, implementation technologies, or product decisions.
- Do not repeat the full problem statement, personas, JTBD, or metrics.
- Do not invent statistics, user behaviors, urgency, market conditions, or demographic characteristics.
- Distinguish documented facts from assumptions.
- If evidence for a required element is unavailable, state "N/A: insufficient evidence" rather than filling the gap with inference.

### Problem statement

Define the primary, evidence backed problem the product is intended to address. The problem must describe a user or business problem, not a solution, feature, assumption, symptom, or broad societal issue.

Include:

- **Affected population:** who experiences the problem, based only on evidence
- **Current situation or behaviour:** what happens today, and in what context
- **Core problem:** what specifically is going wrong
- **Impact or consequence:** why the problem matters, and what measurable effect it causes
- **Frequency, severity, magnitude:** quantitative evidence where available, never invented
- **Existing workarounds:** how users currently cope, and why that coping is inadequate
- **Why now:** only where supported by evidence
- **Problem boundary:** what is and is not part of the problem

### Stakeholders

### Personas

### Job To Be Done

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

# Not covered by this skill

Do not generate these sections. If the user asks for one, say it is not covered here.

1. Risk and legal compliance
2. Accessibility standards
3. Terms of service
4. GTM and rollout strategy
5. Monetization, pricing and impact
6. Post-launch support

# Guardrails

- Stay within the evidence the user provided
- Never invent research, users, goals, pain points or requirements
- Never write a section owned by a delegated skill
- Never treat a plausible answer as a substitute for a missing input
- Distinguish missing, unverifiable, and not applicable
- Report a gap rather than filling it
- Overwrite the output file on each run rather than patching a previous version
- Do not add features the user did not ask for and the research does not support

## Before Submitting, Verify

1. Every Job To Be Done row maps to at least one epic.
2. Every epic maps to a named persona.
3. Nothing listed as out of scope appears in the epics or user flows.
4. Every metric traces to a problem statement or a job to be done.
5. Every section in the Output list is present, in order.
6. Every section in the Output list is present and in the correct order.
7. Any section marked N/A names the input that would fill it, and no later section depends on it.
8. No feature, persona, goal or pain point appears that is not traceable to the inputs.
   Skip any check that depends on a section marked N/A. Fix any failures before returning the document.
