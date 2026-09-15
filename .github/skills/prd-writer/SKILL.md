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

- Use a table for core features, JTBD, in and out of scope features and metrics.
- Use a flow chart for the SAD. If the SAD is provided as an image or a format you cannot read as text, embed or reference it as given. Do not redraw it. Insert the user flows exactly as the user flow skill returns them.
- Create a cover page with product name, date & time.


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