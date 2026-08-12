# Power CAT Architecture Advisor Plugin

Power CAT style architecture recommendation plugin for Power Platform scenarios.

## Skill

### /powercat-pp-architecture-advisor

Transforms categorized discovery answers into a comprehensive architecture recommendation similar to an in-person Power CAT Solution Architect review.

What it produces:

- Architecture recommendation with rationale and diagram
- Security and governance baseline
- Data and integration design
- ALM and operational model
- 30/60/90 day implementation roadmap
- Prioritized implementation backlog
- Decision log and risk register

## Discovery Input Model

The skill infers requirements from the user's scenario, conversation, and uploaded requirements documents. It asks three scenario-specific questions that can be answered together in one paragraph, then presents labelled assumptions that the user can accept or overwrite.

The plugin also includes an internal reusable question bank at:

- references/architecture-questionnaire.md

The question bank guides the LLM's selection of the three highest-value questions; users do not need to complete it. Further questions are reserved for safety, legal, platform-fitness, or technically divergent blockers that cannot safely be assumptions.

## Local Test

```bash
claude --plugin-dir /path/to/powercat-architecture-advisor
```

Then prompt:

- "Design a Power Platform architecture for this scenario"
- "Run a Power CAT style architecture assessment"
- "Recommend the best pattern using my questionnaire answers"

## Copilot Studio

To deploy this skill with an agent powered by the GitHub Copilot harness, use the package builder and configuration guide in [copilot-studio/](copilot-studio/README.md). The generated upload ZIP is written to the ignored `build/copilot-studio/` directory.

## Public Repo Readiness

- No internal endpoints
- No customer data included
- No credentials or secrets
- MIT metadata aligned for marketplace contribution
