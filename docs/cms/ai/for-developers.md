# 📖 对照翻译：AI for developers

> Source: `docusaurus/docs/cms/ai/for-developers.md`  
> Upstream SHA: `e1d9c3545a142b7dd5b8a351a7e215c5e82da5dc`

**Original:** The Strapi documentation site includes free AI-powered tools including an AI toolbar, chatbot powered by Kapa, `llms.txt` files, and MCP servers to help developers learn and integrate Strapi more effectively.

**中文译文:** Strapi Documentation 提供一组面向开发者的免费 AI 工具，包括 AI toolbar、Kapa-powered chatbot、`llms.txt` 系列文件，以及 MCP servers，帮助开发者更高效地学习、查询和集成 Strapi。

## AGENTS.md

**Original:** The `strapi/strapi` and `strapi/documentation` repositories include `AGENTS.md` files for AI-based tooling.

**中文译文:** `strapi/strapi` 与 `strapi/documentation` repository 都提供 `AGENTS.md`，可作为 AI coding / documentation agent 的项目级指导规则。

## AI toolbar

**Original:** Every docs page includes an AI toolbar with actions for Markdown, ChatGPT, Claude, and LLMs files.

**中文译文:** 每个 documentation page 标题下方都有 AI toolbar，常用 action 包括：
- **Copy Markdown**：复制当前页面的 clean Markdown；
- **View as Markdown**：打开页面的 `.md` 版本；
- **Open with ChatGPT**：打开新 ChatGPT conversation，并带入当前页面 URL；
- **Open with Claude**：打开 Claude conversation，同时复制 prompt；
- **View LLMs.txt / LLMs-code.txt / LLMs-full.txt**：打开适合 AI 工具使用的聚合文本文件。

### Copy Markdown

**Original:** The copied Markdown is the same clean content exposed by the page's `.md` URL, with layout components resolved to plain Markdown.

**中文译文:** **Copy Markdown** 获取的是页面对应 `.md` URL 的 clean Markdown，复杂 layout components 会被转换为普通 Markdown，适合直接粘贴到 ChatGPT、Claude、Gemini 等 AI assistant 中。

**Original:** In Markdown mode, Copy Markdown and View as Markdown are replaced by a View this page as .md button.

**中文译文:** 在 **Markdown mode** 中，toolbar 不再显示 Copy Markdown / View as Markdown，而使用 **View this page as .md** 按钮。

### Open with LLM

**Original:** ChatGPT and Claude actions open a conversation prefilled with a prompt containing the current page URL.

**中文译文:** **Open with ChatGPT** / **Open with Claude** 会生成包含当前文档 URL 的 prompt，并根据 browser language 自动本地化。Claude 版本还会把 prompt 复制到 clipboard。

## AI chatbot

**Original:** The documentation chatbot is powered by Kapa and draws from docs, community forums, blog posts, and other Strapi resources.

**中文译文:** Documentation 中的 Ask AI chatbot 由 Kapa 提供，会综合 Strapi docs、community forums、blog posts 等官方 / 社区资源回答问题。

### Sidebar entry

**Original:** Click Ask AI in the left sidebar to start a general Strapi conversation.

**中文译文:** 点击左侧 sidebar 的 **Ask AI**，可以围绕 Strapi 任意主题发起对话，例如 installation、REST population、admin customization 等。

**Original:** Deep thinking mode is available for more complex questions.

**中文译文:** 对复杂问题，可以启用 **deep thinking mode**，获得更深入但响应更慢的结果。

### Code-block entry

**Original:** Code blocks show an Ask AI action on hover.

**中文译文:** Documentation code block 在 hover 时会显示 **Ask AI**；点击后会把该 snippet 作为 context，适合询问配置含义、API response、lifecycle hook 等代码细节。

### AI mode

**Original:** AI mode splits the page into documentation on the left and an AI assistant panel on the right.

**中文译文:** 每个页面都可以切换到 **AI mode**：左侧继续显示 documentation，右侧显示 AI-generated summary 与 question box，可边阅读边提问。

## LLMs text files

| File | 中文说明 | 适用场景 |
|---|---|---|
| `llms.txt` | 全部页面的简洁、link-rich overview | 高层 context、导航、RAG pipeline |
| `llms-full.txt` | 完整文档合并为一个大文件 | Context window 足够大时提供全站 context |
| `llms-code.txt` | 按页面组织的全部 code examples | Code generation、migration、API discovery |

**Original:** `llms.txt` is best for broad context without spending too many tokens.

**中文译文:** `llms.txt` 适合作为低 token 成本的全站目录与语义入口。

**Original:** `llms-full.txt` provides full documentation content but is large.

**中文译文:** `llms-full.txt` 提供完整 documentation body，但文件很大，需确认目标 model 的 context window 足够。

**Original:** `llms-code.txt` focuses on code snippets and includes source page URLs.

**中文译文:** `llms-code.txt` 聚合代码示例，并保留 source page URL / anchor，方便 traceability。

## MCP servers

**Original:** Strapi provides 2 MCP servers.

**中文译文:** Strapi 当前提供两种 MCP server：
- **Strapi MCP server**：连接具体 Strapi instance，用自然语言管理 content；
- **Docs MCP server**：连接官方 documentation，为 IDE / AI assistant 提供最新 Strapi context。

**Original:** The Strapi MCP server also exposes Media Library tools.

**中文译文:** 除 schema-driven content tools 外，Strapi MCP server 还暴露 Media Library assets / folders 相关 tools。

## Tips for Docs MCP

**Original:** Prefix docs questions with `Use the strapi-docs MCP server to answer:`.

**中文译文:** 为避免 assistant 使用可能过时的训练数据，建议 docs-related prompt 以：

`Use the strapi-docs MCP server to answer:`

开头。

**Original:** Include the page URL and Strapi version, and prefer documented APIs over private internals.

**中文译文:** 提问时建议：
- 附上相关 page URL；
- 明确 Strapi version，例如 Strapi 5；
- Code snippet 最好带 source；
- 优先要求使用 documented public API，而不是 private internals。

## Inki

**Original:** Inki is a Claude Code plugin for contributing to Strapi documentation, bundling prompts, templates, skills, editorial rules, and review workflows.

**中文译文:** **Inki** 是 Strapi Documentation 团队提供的 Claude Code plugin，包含：
- 内容调研与路由 skills；
- prompts；
- templates；
- authoring guides；
- editorial rules；
- review / code verification workflow；
- 创建 pull request 的完整流程。

**Original:** Even without Claude Code, its Markdown prompts and guides can be reused with other agents.

**中文译文:** 即使不使用 Claude Code，也可以让 Cursor、GitHub Copilot、Cline、Windsurf 等 AI agent 读取 Inki folder 中的 Markdown prompts、references 与 templates。
