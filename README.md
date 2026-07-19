# 🛠️ skills.sh MCP Server

[![npm version](https://badge.fury.io/js/skills-mcp-server.svg)](https://badge.fury.io/js/skills-mcp-server)

An unofficial [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server for the [skills.sh](https://skills.sh) ecosystem. This server empowers your AI agents (like Claude Code, Antigravity-cli, or Cursor) to autonomously search, evaluate, and install the most relevant skills directly from the skills.sh catalog.

---

## ✨ Features

- **Zero-Config & No Auth:** Uses public endpoints—no Vercel tokens or API keys required.
- **AI-Native & Self-Documenting:** Natively embeds detailed workflow instructions via MCP Prompts and Resources so your LLM always knows exactly how to search effectively.
- **4 Powerful Tools:**
  - `search_skills`: Semantic search through the catalog.
  - `get_skill_details`: Deep-dive analytics (installs, platforms, history).
  - `get_popular_skills`: Discover trending and hot skills.
  - `get_install_command`: Instantly generate `npx` installation commands.

## 🚀 Quick Start (Recommended)

### For Claude Code
You can install this directly into Claude Code with a single command:
```bash
claude mcp add skills-sh -- npx -y skills-mcp-server
```

### For Claude Desktop & Cursor
Add the following to your MCP client configuration (e.g., `claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "skills-sh": {
      "command": "npx",
      "args": [
        "-y",
        "skills-mcp-server"
      ]
    }
  }
}
```

### Global Installation (Optional)
If you prefer not to use `npx` every time, you can install it globally:
```bash
npm install -g skills-mcp-server
```
Then use `skills-mcp-server` as your command instead of `npx`.

## 💻 Running from Source

If you prefer to run the server locally:

1. Clone this repository.
2. Install dependencies: `npm install`
3. Build the project: `npm run build`
4. Add the absolute path to your MCP client config:

```json
{
  "mcpServers": {
    "skills-sh": {
      "command": "node",
      "args": [
        "/absolute/path/to/your/skills-mcp-server/build/index.js"
      ]
    }
  }
}
```

## 🧠 How the AI Uses This Server

This server is designed to be fully self-documenting for LLMs.

When your agent connects, it automatically gains access to:
1. **Rich Tool Descriptions:** Tools contain explicit instructions telling the LLM to generate diverse keywords, loop searches, and thoroughly vet results before recommending them.
2. **MCP Resources:** Exposes a `skills-sh://agent-instructions` resource. Advanced clients can automatically read this to understand the full step-by-step searching workflow.
3. **MCP Prompts:** Exposes a `skills-search-workflow` prompt. Users can invoke this manually in supported clients to force the LLM into a highly optimized "Skill Search Mode".

---

### Acknowledgements

*Core API discovery and initial implementation credit goes to [brandonqr/skillsh-mcp](https://github.com/brandonqr/skillsh-mcp).*
