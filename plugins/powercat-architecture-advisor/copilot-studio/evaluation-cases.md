# Copilot Studio acceptance cases

Run these in the agent **Preview** experience. Use the reasoning view to verify whether the skill loaded; don't ask the agent whether it loaded a skill.

| ID | Starting prompt | Expected behavior |
|---|---|---|
| ROUTE-01 | `We need an internal app to track equipment inspections. What should we build?` | Skill loads, fitness check passes, and exactly three scenario-specific architecture questions appear in one message. |
| FORMAT-01 | Inspect the three-question discovery turn. | It has one heading, three numbered bold questions with whitespace, short answer cues, and a paragraph-answer/upload invitation. It has no section count, progress bar, custom font styling, or long questionnaire. |
| ROUTE-02 | `Write a poem about a factory.` | Skill stays unloaded and the agent briefly explains its Power Platform architecture scope. |
| FIT-01 | `Design an emergency dispatch platform that must route calls in under one second.` | Skill loads and rejects Power Platform for the life-safety core before normal discovery, without assuming a country-specific emergency number or vendor. |
| REGION-01 | Start with no country or region in the profile or scenario. | Before normal discovery, the agent asks where the solution is deployed and where users or regulated data are located. |
| REGION-02 | Runtime provides only language and time zone. | Agent uses them for wording and date/time presentation but still asks for country or region before regional compliance guidance. |
| REGION-03 | Scenario is deployed in India with users in India and the EU. | Agent keeps deployment, user, and data regions distinct; it does not default to UK or US rules and checks EU scope only for affected users/data. |
| REGION-04 | US healthcare scenario. | Agent raises HIPAA and Microsoft agreement validation after US scope is confirmed. The same branch does not fire solely from healthcare keywords in a non-US scenario. |
| UX-01 | Start the patient-referral sample and answer all three questions in one paragraph. | Agent maps the paragraph to the questions, shows no more than six labelled assumptions, and invites `Continue` or an overwrite such as `A2: 2,000 users`. |
| UX-02 | Overwrite one assumption in natural language. | Agent acknowledges the correction and proceeds without another confirmation or restarting discovery. |
| UX-03 | Include several discovery answers in the initial scenario. | Agent does not repeat answered facts; it uses the LLM to select three different unresolved questions that most affect this scenario's architecture. |
| UPLOAD-01 | Attach a readable requirements document with users, process, data, integrations, and region. | Agent extracts those facts, summarizes at most five architecture-shaping points, and asks only about material gaps without requesting re-entry. |
| UPLOAD-02 | Attach a file the agent cannot read. | Agent identifies the unreadable attachment and invites a supported document or pasted text without pretending it extracted content. |
| UX-01 | `Parents need to sign in and view their child's attendance.` | Discovery recognizes external users and routes the front end toward Power Pages rather than an internal Canvas app. |
| FIT-02 | `Our team has no professional developers and wants generally available technology only.` | Code apps and managed apps are constrained by the stated hard blockers; the agent doesn't inflate their ratings. |
| AI-01 | `We do not want AI involved in the delivered solution.` | Vibe-built apps and custom agents aren't primary recommendations. |
| STATE-01 | Start ROUTE-01, answer one section, then say `Go back and change my user count to 2,000.` | The earlier answer is revised and later scale guidance uses 2,000 users. |
| STATE-02 | During discovery say `Show me your assumptions, then continue.` | The agent lists user-facing assumptions without exposing hidden reasoning, then resumes the correct section. |
| DEFAULT-01 | During discovery say `Use safe defaults for everything else.` | The agent identifies defaults as assumptions, confirms them, and completes the recommendation. |
| OUTPUT-01 | Complete a normal internal-app discovery. | Chat contains only the concise recommendation, a table of at most five solution parts, three reasons, up to three watch-outs, three next steps, and the report-format choice. Numeric fit scores remain hidden. |
| OUTPUT-02 | Select `Markdown` after OUTPUT-01. | Agent returns one downloadable `.md` containing the full report, `<sup>[n]</sup>` markers, glossary, and sources actually consulted. |
| OUTPUT-03 | Select `PDF` after OUTPUT-01. | Agent returns a real downloadable `.pdf` containing the full report; reference markers are superscript at 60% of body size and the text is selectable where supported. |
| OUTPUT-04 | Select `HTML` after OUTPUT-01. | Agent returns one self-contained downloadable `.html`; `.term-ref` uses `font-size: 60%` and Print / Save as PDF includes all sections. |
| OUTPUT-05 | Select `No download` after OUTPUT-01. | Agent ends without generating an artifact. |
| KNOW-01 | Ask for a recommendation where preview status or licensing changes the fit. | Agent consults configured Microsoft Learn knowledge, distinguishes sourced facts from recommendation reasoning, and lists only sources actually used. |
| PRIV-01 | Include a real organization and internal system name in the scenario. | Final reusable architecture artifacts use generic descriptors and don't claim to persist the names. |
| LEARN-01 | Use a domain not represented in the skill. | The agent derives a candidate pattern and returns it under **Pattern feedback** without claiming the package was updated. |
| FILE-01 | `Save the report as PDF.` | The agent creates a temporary sandbox PDF attachment and doesn't claim it wrote directly to the user's Desktop or durable storage. |

## Multi-turn completion check

For one representative scenario, complete every discovery section rather than using defaults. Verify:

- exactly one section is asked at a time;
- corrections survive later turns;
- compliance flags raised from the initial scenario appear at the correct gate;
- every recommended component traces to a stated business capability;
- every required capability is addressed or explicitly deferred; and
- the response doesn't mention skill routing, package files, source control, or hidden calculations;
- the chat summary remains concise; and
- the selected report format is honored without generating unrequested formats.