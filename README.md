# prd-writer

An Agent Skill that writes product requirement documents from a research report and a system architecture diagram.

`prd-writer` does not write the whole document. It owns some sections and delegates the rest to smaller skills beside it. Where a delegated skill is missing, that section is marked N/A rather than invented.

The setup follows the open Agent Skills standard, and has been tested in GitHub Copilot in VS Code.

## Structure

```
.github/skills/
  prd-writer/      the PRD skill
inputs/            your research report and SAD (not in this repo)
outputs/           the generated PRD, when writing locally
```

The following sections are written by prd-writer itself: cover page, introduction, problem statement, stakeholders, proposed solution, epics, out of scope, dependencies and assumptions. Personas, jobs to be done, user flows, metrics are delegated to separate skills, none of which are included here.

## Running it

Copilot Chat should be set to Agent mode with the SAD image attached, then prompted with something like this:

```
Write a PRD using the prd-writer skill. Research report: #file:inputs/research.md.
The SAD is the attached image. Save it to Notion, do not print it in chat.
```

## The rule that matters

Where a sub skill file is missing or empty, the section is output as N/A. A delegated section is never written by prd-writer itself, even when the user has supplied an input file covering that content.

## Trials

**1. No sub skills present.** Every delegated section came back N/A, and only the sections backed by the research report were written.

**2. A user flows skill added.** The skill loaded and ran, then reported that its own inputs, personas and jobs to be done, had not been provided.

**3. Personas and JTBD supplied as files.** With the inputs the user flows skill depends on now in place, it worked and produced the flows.

The skill used in trials 2 and 3 was written by another group and is not included in this repo.

## MCP connections

The skill writes its output to Notion using a remote MCP server over OAuth, so no API token is stored anywhere.

### Setup

Create `.vscode/mcp.json` in the project root:

```json
{
  "servers": {
    "notion": {
      "type": "http",
      "url": "https://mcp.notion.com/mcp"
    }
  }
}
```

With that file open, a Start button appears above the server. Click it and approve the OAuth prompt in the browser that opens. The redirect goes to 127.0.0.1, which is your own machine.

To confirm it worked, open Copilot Chat, switch to Agent mode, and click the tools icon at the bottom of the chat box. Notion should be listed with its tools underneath. If it is not, restart VS Code.

MCP only works in Agent mode. Regular Copilot Chat does not support it.

### Resources

- Notion MCP: https://developers.notion.com/guides/mcp/overview

## Similar skills and credits

Existing PRD skills we looked at while building this one, and what we took:

- [DivikWu/product-requirement-craft](https://github.com/DivikWu/product-requirement-craft) — their Phase 5 re-reads the relevant template right before generating, because long conversations push earlier context out of the window. Step 4 of our Process does the same: it re-reads each section's rules before writing that section.
- [TayaIntelligence/skills](https://github.com/TayaIntelligence/skills) — their `technical-pm` produces Given / When / Then acceptance criteria covering happy path, boundaries and failure. Our epics section now requires the same format, which is what makes our own "acceptance criteria are testable" check verifiable.
- [iannuttall/claude-agents prd-writer](https://github.com/iannuttall/claude-agents/blob/main/agents/prd-writer.md) — two things. Unique requirement IDs for traceability, which became our EP-001 epic IDs. And their output rules forbidding dividers, conclusions and footers, which fixed a run where a verification summary was appended to the document.
- [jamesrochabrun/skills prd-generator](https://github.com/jamesrochabrun/skills/blob/main/skills/prd-generator/SKILL.md) — reviewed for its `references/` structure and validation script. We took nothing from it in the end, since both were larger refactors than this build had room for.

### What is different here

Every skill above writes the whole document itself. This one delegates personas, jobs to be done, user flows, metrics and competitor differentiators, and marks a section N/A when its skill is absent rather than filling the gap.

## Inputs

The inputs are not included in this repo. To run the skill, an `inputs/` folder is needed containing a research report in markdown and a SAD in any readable format. Personas and JTBD are optional, and without them the user flows section returns N/A, which is the intended behaviour.

## Quality analysis

Results from the skills quality scorer are in `analysis/`.

## Credits

Built by AnitaB.
- Mahlet Hiluf
- Lucy Gacema
- Deborah Wakere
- Emma Mwelwa
- Gladys Ouma
- Nagaba Shallot
- Andy Laique
- Phillipine Giramata
