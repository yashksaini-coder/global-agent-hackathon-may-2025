# Best Use of Potpie 🥧

We’re thrilled to be part of the Global Agent Hackathon with Agno! 🧠⚙️

We're offering **TBD** for the best use of [Potpie](https://github.com/potpie-ai/potpie) during the hackathon.

Potpie is an **open-source agent platform** built specifically for developers and their codebases. It turns a single prompt into a powerful, context-aware agent that understands your entire repo.

You can pair Potpie with Agno's MCP server to build agents that:
- Understand and navigate your codebase with a knowledge graph
- Perform debugging, system design, test generation, and more
- Connect with tools like GitHub, Jira, and Linear to create dev workflows

If you’ve ever wanted a dev tool that *actually* understands your stack — Potpie is it.

---

## How Potpie Works

Potpie indexes your codebase and builds a semantic **knowledge graph**, allowing agents to:
- Traverse and reason across code
- Link functions, classes, APIs, components, and files
- Provide rich context-aware answers and workflows

Potpie integrates tightly with:
- GitHub (repos, PRs, commits)
- Linear (issues, tickets)

Use Potpie with Agno’s MCP to inject deep codebase intelligence into your agents.

---

## Building Custom Agents

### Potpie Tools

You can create custom agents from a single prompt on app.potpie.ai and those agents select the tools on their own, but sometimes we need to include or remove certain tools while iteration on the agent outputs, prompts might need to be updated to include specific guidance for their execution plan etc  For those times, here are the tools that Potpie agents use internally and a brief description about their usage. 

- **get_code_from_probable_node_name**: Fetches code based on a likely node name match in the knowledge graph.
- **get_code_from_multiple_node_ids**: Returns code snippets for a list of node IDs.
- **ask_knowledge_graph_queries**: Enables natural language querying over the knowledge graph.
- **get_nodes_from_tags**: Lists nodes associated with specific tags like `API`, `Database`, etc.
- **get_code_graph_from_node_id**: Generates a local dependency graph starting from a specific node ID.
- **change_detection**: Analyzes code changes and summarizes diffs with metadata.
- **get_code_file_structure**: Returns the directory and file structure of the ingested codebase.
- **get_node_neighbours_from_node_id**: Retrieves neighboring nodes in the knowledge graph from a given node ID.
- **get_linear_issue**: Fetches details of a Linear issue by ID. (requires linear API key to be set in Key Management screen) 
- **update_linear_issue**: Updates status, priority, or description of a Linear issue.(requires linear API key to be set in Key Management screen) 
- **intelligent_code_graph**: Generates a filtered code graph, good for reducing context in larger codebases. 
- **think**: A reflective reasoning tool for maintaining context or brainstorming within an agent's workflow.
- **github_create_branch**: Creates a new GitHub branch with metadata context.
- **github_update_branch**: Pushes code updates to an existing GitHub branch.
- **github_create_pull_request**: Opens a GitHub PR with generated title, description, and branch metadata.
- **github_add_pr_comments**: Adds inline review comments to a GitHub PR based on context or code diffs.


### Example Dev Workflows 

- Generate unit/integration tests
- Suggest design improvements
- Summarize PRs
- Auto-create GitHub issues or Linear tickets based on Potpie agent results
- Review workflows: Extract change impact and recommend fixes
- Automate integrations that follow the same patterns (E.g. Adding a memory provider into an Agent framework etc) 

### Ingestion

- GitHub Repos Issues & Pull Requests
- Ticketing Systems (Linear)
- Web pages (Direct link) 

---
## Generating an API Key

To generate an API key, follow these steps:

1. Navigate to [app.potpie.ai](https://app.potpie.ai).
2. Click on your username in the bottom left corner.
3. Select **Key Management** from the menu.
4. In the "API Key Management" section, click on **Generate API Key**.

Your API key will be created and displayed for use.

## Using the API

Postman collection is hosted [here](https://drive.google.com/file/d/1DMF2A5oy8zeNb0xQMUn82fcF2CVvc__L/view?usp=sharing)
Video walkthrough [here](https://x.com/runtimeHorror/status/1897144432404914215)

To use the API, follow these steps:

1. **Base URL**: Use `https://production-api.potpie.ai/` as the base URL.

2. **Parse API**:
   - **API Path**: `/api/v2/parse`
   - **Request Method**: POST
   - **Request Body**:
     ```json
     {
       "repo_name": "potpie-ai/potpie",
       "branch_name": "main"
     }
     ```
   - The Parse API will return a **project ID**.

3. **Get Parsing Status**:
   - **API Path**: `/api/v2/parsing-status/{project_id}`
   - **Request Method**: GET
   - **Query Parameters**:
     - `project_id`: The ID returned from the Parse API.
     - `x-api-key`: Your API key (in the header).
   - Wait until the project status is "ready".


### List of Agents

You can choose from the following agents:

- **Codebase Q&A Agent**: `id="codebase_qna_agent"`
- **Debugging with Knowledge Graph Agent**: `id="debugging_agent"`
- **Unit Test Agent**: `id="unit_test_agent"`
- **Integration Test Agent**: `id="integration_test_agent"`
- **Low-Level Design Agent**: `id="LLD_agent"`
- **Code Changes Agent**: `id="code_changes_agent"`
- **Code Generation Agent**: `id="code_generation_agent"`

- For custom agents created on the Potpie dashboard, you can simply copy their Agent id using the copy button on the Custom Agent screen. 

4. **Send Message**:

   - **API Path**: `/api/v2/project/{{project_id}}/message`
   - **Request Method**: POST
   - **Request Body**:
     ```json
     {
       "content": "your_message_content",
       "node_ids": [] //leave this empty
     }
     ```
   - **Query Parameters**:
     - `conversation_id`: The ID of the conversation created in the previous step.
     - `x-api-key`: Your API key (in the header).

Note: 
* Try to use the /parse API sparingly, every invocation of this API will trigger the processing step if the knowledge graph is not upto date.
* We recommend that once you have a project in the 'ready' state, you hardcode the project id in this API, this avoids the added latency of parsing the codebase everytime unnecessarily. 


---

## 🎥 Need Inspo?

Here’s a [video walkthrough](https://youtu.be/a4rInO0xa54?feature=shared) of how Potpie can automate integration work in repos like Langflow. 

---

## 💬 Questions?

Join our [Discord](https://discord.com/invite/ryk5CMD5v6) — we’re happy to help you build custom agent magic.
