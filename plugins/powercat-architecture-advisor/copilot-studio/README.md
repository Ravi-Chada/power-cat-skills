# Copilot Studio deployment

This folder builds the Power CAT Architecture Advisor as a skill package for an agent powered by the GitHub Copilot harness in the new Microsoft Copilot Studio experience.

## Build the package

From the repository root, run:

```powershell
& 'plugins\powercat-architecture-advisor\copilot-studio\build-package.ps1'
```

The ignored `build/` directory receives:

```text
build/copilot-studio/
├── powercat-pp-architecture-advisor/
│   ├── SKILL.md
│   └── references/
└── powercat-pp-architecture-advisor.zip
```

The builder keeps the original skill authoritative. It creates a deployment copy that:

- retains only portable skill frontmatter;
- adds Copilot Studio conversation and state rules;
- treats bundled references as read-only;
- replaces runtime self-modification with maintainer-reviewed pattern feedback;
- returns a concise chat summary and generates the user's selected Markdown, PDF, or HTML report in the sandbox; and
- validates that all major workflow sections remain present.

## Configure the existing agent

1. Confirm the agent uses the **GitHub Copilot harness**. Skills in this format aren't supported by the standard harness.
2. Open the agent's **Build** tab.
3. Paste [agent-instructions.md](agent-instructions.md) into the agent **Instructions** editor.
4. In the components panel, open **Skills** and select **Upload a skill**.
5. Upload `build/copilot-studio/powercat-pp-architecture-advisor.zip`.
6. Keep the Microsoft Learn website knowledge sources for Power Platform, Power Apps, Power Automate, Power Pages, and Microsoft Copilot Studio.
7. Enable file or attachment input for the agent and intended channel so users can submit requirements documents. The exact control can vary by Copilot Studio release and channel; verify it in the current agent settings rather than assuming every published channel supports uploads.
8. Open **Preview** and run the cases in [evaluation-cases.md](evaluation-cases.md), including `UPLOAD-01` and `UPLOAD-02` with representative supported and unsupported files.
9. Inspect the reasoning view during tests. Confirm the skill loads for architecture requests and stays unloaded for unrelated prompts.
10. Add the agent to a Power Platform solution for Dev, Test, and Production movement.
11. Publish only after the acceptance cases pass in the target environment and its attachment behavior is verified.

## Initial deployment boundaries

- Output is a concise chat summary plus an optional Markdown, PDF, or HTML download generated in the sandbox.
- Requirements-document ingestion depends on file attachments being enabled and supported by the active channel. When unavailable, users can paste relevant text instead.
- Discovery state lasts for the active conversation.
- No conversation data or new pattern is persisted.
- Microsoft Learn website knowledge grounds current product facts; no action tool is required for temporary downloads.
- Building, testing, evaluating, and using the agent consumes Copilot Credits.

Add persistence later through an explicitly approved Dataverse or Power Automate tool. Do not enable broad memory as a substitute for a governed discovery record.

## Update an uploaded skill

1. Change the authoritative skill or its references in the plugin.
2. Run `build-package.ps1` again.
3. In **Build → Skills**, open the uploaded skill, select **... → Replace**, and choose the new ZIP.
4. Rerun the acceptance cases before publishing.