# North Star AI – example repo

An example repository that accompanies the article **"Fra chat til agent: Når GitHub Copilot får tilgang til systemene du jobber i"** (in Norwegian).

It shows how instructions, skills, prompts, wiki guidelines and MCP configuration fit together when GitHub Copilot is used as an agent in Dynamics 365 / Power Platform development.

> **This is an example, not a working project.** North Star AI is a fictional project, URLs and names are placeholders, and nothing here is a recommendation. How much access an agent should get depends on your own risk assessment. See the last section of the article.

## Structure

| Path | What it is |
|---|---|
| `.github/instructions/` | **Instructions** set the frame: default Azure DevOps project, Dataverse environments and safety rules. Always part of the agent's context. |
| `.github/skills/northstar-work-item/` | A **skill** describes *how* a type of task is done, here how a User Story looks in the project (business-focused title, Given/When/Then, linked Feature, preview before creation). |
| `.github/prompts/review-power-automate.prompt.md` | A **prompt** that reviews a Power Automate flow retrieved from Dataverse against the developer guidelines, the work item and Microsoft Learn. |
| `.vscode/mcp.json` | **Workspace** MCP configuration. Microsoft Learn MCP is not here on purpose: it is low risk and installed globally. Azure DevOps and Dataverse follow the project. |
| `environments.json` | Named Dataverse environments for the local Dataverse MCP: `dev` is writable, `test` and `prod` are read-only. |
| `Dynamics.wiki/` | Mirrors the Azure DevOps wiki. `CoE/Power-Automate.md` holds the general Power Automate development practice used as the first source in the review's authority order. |
| `Dynamics.Solutions/` | Mirrors the Azure DevOps solutions repo: The project's dynamics solutions would normaly live here. |

## How the pieces work together

* **Instructions** set the frame.
* The **prompt** says what we want to do.
* The **skill** describes how we do it.
* The **MCP** gives the agent access to the system.

## To try it yourself

1. Replace the placeholder URLs in `environments.json` and `dataverse.instructions.md` with your own environments.
2. Create your own Azure DevOps project and change the default project in `azure-devops.instructions.md`.
3. Install the MCPs your setup needs. This repo only contains the workspace configuration.
    - The local Dataverse MCP used in the article is [`jaj-dataverse-dev-mcp`](https://www.npmjs.com/package/jaj-dataverse-dev-mcp)
4. Check which tools the agent actually gets. An MCP being able to do something does not mean the agent should be allowed to.

## License

MIT