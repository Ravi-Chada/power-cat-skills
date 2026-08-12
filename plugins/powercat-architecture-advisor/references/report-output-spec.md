# Detailed report output specification

Use this specification whenever the user selects a downloadable detailed report.

## Required sections

Include these sections in this order:

1. Scenario, confirmed regional context, and confirmed assumptions
2. Recommended solution mapped to business capabilities
3. Options considered with Strong fit / Good fit / Fit / Doesn't fit and tradeoffs
4. Architecture diagram or a plain-text component flow when the selected format cannot render Mermaid
5. Component and shared data model detail
6. Security, compliance, governance, and ALM baseline
7. Risk register with preventive and contingency actions
8. 30/60/90-day roadmap and quick wins
9. Prioritized backlog
10. Decision log
11. Next steps
12. Glossary
13. Sources consulted

## Microsoft Learn grounding

Use the configured Microsoft Learn website knowledge sources for current claims about Power Platform, Power Apps, Power Automate, Power Pages, and Microsoft Copilot Studio.

- Ground product capability, availability, preview status, connector support, licensing impact, and regional availability when those facts materially affect the recommendation.
- Prefer the Microsoft Learn knowledge sources over model memory for these claims.
- Do not invent a citation or URL. If retrieval does not provide a source, mark the claim **Confirm before implementation**.
- Add a **Sources consulted** section containing only sources actually used. Include page title and URL when the runtime provides them.
- Keep business reasoning and scenario-specific recommendations distinct from sourced product facts.
- State the deployment region, user regions, and data-residency regions separately. Do not infer any of them from language or time zone.
- Include region-specific legal or regulatory considerations only when the region and scope are confirmed; label them for specialist validation rather than as legal advice.

## Numbered terms and visual weight

Mark a technical term only on first use and keep markers sequential from `[1]`.

- **Chat and Markdown:** render the marker as inline HTML superscript, for example `Dataverse<sup>[1]</sup>`. This gives the marker lower visual weight in renderers that support inline HTML while remaining readable as source text.
- **HTML:** wrap markers in `<sup class="term-ref">[1]</sup>` and include `.term-ref { font-size: 60%; line-height: 0; vertical-align: super; }`.
- **PDF:** draw markers as superscript at exactly 60% of the surrounding text size. For 10-point body text, use a 6-point marker.
- The glossary number uses normal glossary text size so it remains accessible.

Do not reduce the technical term itself to 60%; reduce only its numbered marker. Making all referenced terms 60% would harm readability and incorrectly make product names look unimportant.

## Markdown

- Create `<scenario-slug>-architecture-report.md` as UTF-8 Markdown.
- Use headings, compact tables, bullets, and a fenced Mermaid block.
- Use `<sup>[n]</sup>` markers.
- Include the full report, not the concise chat summary.

## HTML

- Create `<scenario-slug>-architecture-report.html` as a self-contained UTF-8 document.
- Follow `references/html-report-spec.md` for layout and print behavior.
- Include the `.term-ref` style exactly as specified above.
- Ensure Print / Save as PDF presents every report section, not only the active tab.

## PDF

- Create `<scenario-slug>-architecture-report.pdf` as a valid PDF document.
- Use a PDF library available in the Copilot Studio sandbox and inspect the resulting file before returning it.
- Use a readable page size, margins, repeated table headings, page numbers, and sensible page breaks.
- Render the architecture as a simple component-flow diagram when possible; otherwise include a readable component-flow table.
- Use 60% superscript markers and include the complete glossary.
- Never produce a screenshot-only PDF. Text must remain selectable when the library supports it.

## Delivery

Return exactly the selected format as a downloadable attachment. Do not create all formats unless the user asks for more than one. Generated files are temporary; advise the user to download the attachment if they need to retain it.