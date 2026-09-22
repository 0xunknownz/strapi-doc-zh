# 📖 对照翻译：Docs MCP server

> Source: `docusaurus/docs/cms/ai/docs-mcp-server.md`  
> Upstream SHA: `4afd87ef1cbd7d9997ccbc3056406fb28bdb1aef`

**Original:** A Docs MCP server exposes the Strapi documentation to AI coding tools. Connect it to your IDE to get Strapi-aware code suggestions and answers.

**中文译文:** Strapi Docs MCP server 通过 Model Context Protocol 把完整 Strapi documentation 提供给 AI coding tools。连接 IDE 后，AI assistant 可以直接查询最新 Strapi guides、API references 与 code examples，而不是只依赖模型训练数据。

**Original:** The Docs MCP server is powered by Kapa, the same service behind the documentation site's Ask AI button.

**中文译文:** Docs MCP server 由 Kapa 提供，与 Strapi documentation 网站中的 **Ask AI** 使用同一 documentation knowledge source。

**Original:** Strapi offers 2 MCP servers: Docs MCP and Strapi MCP for content management.

**中文译文:** Strapi 当前有两类 MCP server：
- **Docs MCP server**：提供 documentation context；
- **Strapi MCP server**：连接具体 Strapi instance，用于 content management。

## Compatible tools

**Original:** Works with MCP-compatible tools such as Cursor, VS Code + GitHub Copilot, Claude Code, and Windsurf.

**中文译文:** 兼容支持 MCP 的工具，包括 Cursor、VS Code + GitHub Copilot、Claude Code、Windsurf 等。

## Manual configuration

**Original:** Server URL:

`https://strapi-docs.mcp.kapa.ai`

**中文译文:** 手工配置时 MCP endpoint 为：

`https://strapi-docs.mcp.kapa.ai`

### Cursor

```json title=".cursor/mcp.json"
{
  "mcpServers": {
    "strapi-docs": {
      "url": "https://strapi-docs.mcp.kapa.ai"
    }
  }
}
```

### VS Code

```json title=".vscode/mcp.json"
{
  "servers": {
    "strapi-docs": {
      "type": "http",
      "url": "https://strapi-docs.mcp.kapa.ai"
    }
  }
}
```

### Windsurf

```json title="~/.codeium/windsurf/mcp_config.json"
{
  "mcpServers": {
    "strapi-docs": {
      "serverUrl": "https://strapi-docs.mcp.kapa.ai"
    }
  }
}
```

**Original:** Once connected, AI assistants can query Strapi docs for answers, implementation suggestions, and API verification.

**中文译文:** 连接后，AI assistant 可以基于官方文档回答 Strapi 问题、检查 API usage、给出 implementation 建议。

**Original:** For docs questions, explicitly instruct the assistant to use the `strapi-docs` MCP server.

**中文译文:** 为避免工具直接基于过时 training data 回答，可在 prompt 中明确要求：

`Use the strapi-docs MCP server to answer:`
