# prd-agent

An Agent Skill that writes product requirement documents from a research report and a system architecture diagram.

`prd-writer` does not write the whole document. It owns some sections and delegates the rest to smaller skills beside it. Where a delegated skill is missing, the section is marked N/A rather than invented.

The setup follows the open Agent Skills standard, and has been tested in GitHub Copilot in VS Code.

## Structure

```
.github/skills/
  prd-writer/      the assembler, the only skill invoked directly
  user-flows/      user flows section
  personas/        not built yet
  metrics/         not built yet
  jtbd/            not built yet
inputs/            research report and SAD (not in this repo)
outputs/           the generated PRD
```

The following sections are written by prd-writer itself: introduction, problem statement, stakeholders, proposed solution, epics, out of scope, dependencies and assumptions. Personas, jobs to be done, user flows and metrics are delegated.

## Running it

Copilot Chat should be set to Agent mode with the SAD image attached, then prompted with something like this:

```
Write a PRD using the prd-writer skill. Research report: #file:inputs/research.md.
The SAD is the attached image. Save it to outputs/PRD.md, do not print it in chat.
```

## The rule that matters

Where a sub skill file is missing or empty, the section is output as N/A. A delegated section is never written by prd-writer itself.

## Trials

**1. No sub skills present.** Every delegated section came back N/A, and only the sections backed by the research report were written.

**2. The user-flows skill added.** The skill loaded and ran, then reported that its own inputs, personas and jobs to be done, had not been provided.

**3. Personas and JTBD supplied as files.** With the inputs user-flows depends on now in place, it worked and produced the flows.

The skill used in trials 2 and 3 was written by someone else and is not included in this repo.

## Inputs

The inputs are not included in this repo. To run the skill, an `inputs/` folder is needed containing a research report in markdown and a SAD in any readable format. Personas and JTBD are optional, and without them the user flows section returns N/A, which is the intended behaviour.

## Next

The personas skill is the one to build next, since jobs to be done and user flows both depend on it.