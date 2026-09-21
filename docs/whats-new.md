# 📖 对照翻译：What's new in Strapi docs?

> Source: `docusaurus/docs/whats-new.md`  
> Upstream SHA: `cf15f0def9dfd499b7b5d45814c0b135e0336619`

**Original:** What's new in Strapi docs?

**中文译文:** Strapi 文档有哪些新变化？

**Original:** We gave the Strapi documentation a fresh new look and a set of features designed to make reading, navigating, and reusing the docs easier. Here is a quick tour of what changed.

**中文译文:** 我们为 Strapi 文档带来了全新的视觉设计，并加入了一系列功能，让阅读、导航和复用文档内容更加轻松。下面快速了解一下这些变化。

**Original:** **3 reading modes.** Switch any page between **Elegant mode** (the default, fully styled reading experience), **Markdown mode** (a flat, raw-text view that is easy to copy), and **AI mode** (a summary-oriented view built for working with AI assistants). The switcher sits at the top of every documentation page.

**中文译文:** **3 种阅读模式。** 任意页面都可以在 **Elegant mode**（默认模式，提供完整样式的阅读体验）、**Markdown mode**（扁平化的纯文本视图，便于复制）和 **AI mode**（面向 AI 助手协作、以摘要为重点的视图）之间切换。模式切换器位于每个文档页面顶部。

**Original:** **Content-width selector.** Prefer a narrower column for comfortable reading or a wider one to see more at once? A floating control lets you adjust the content width to your taste, and your choice is remembered as you browse.

**中文译文:** **内容宽度选择器。** 喜欢更窄的正文列，以获得更舒适的阅读体验；还是希望加宽内容区域，一次看到更多信息？浮动控件可以按你的偏好调整内容宽度，并会在后续浏览过程中记住你的选择。

**Original:** **Collapsible sidebars.** Both the left navigation and the right "On this page" table of contents can now be collapsed, so you can focus on the content and reclaim screen space whenever you need it.

**中文译文:** **可折叠侧边栏。** 左侧导航栏以及右侧的 “On this page” 页面目录现在都可以折叠。需要专注阅读时，你可以随时收起它们，释放更多屏幕空间。

**Original:** **A brand-new homepage.** The [documentation homepage](/) was redesigned from scratch, with clearer entry points to the CMS and Cloud docs, an interactive API explorer, and quick links to the most popular sections.

**中文译文:** **全新的首页。** [文档首页](/) 已从头重新设计，提供更清晰的 CMS 与 Cloud 文档入口、交互式 API Explorer，以及热门章节的快捷链接。

**Original:** **2-column layout for API references.** The [REST API](/cms/api/rest), [GraphQL API](/cms/api/graphql), and [Document Service API](/cms/api/document-service) reference pages now use a 2-column layout: the description and parameters on the left, and the request and response examples on the right, so you can read and try at the same time.

**中文译文:** **API 参考文档采用双栏布局。** [REST API](/cms/api/rest)、[GraphQL API](/cms/api/graphql) 和 [Document Service API](/cms/api/document-service) 参考页面现在采用双栏布局：左侧展示说明和参数，右侧展示请求与响应示例，让你可以边读边实践。

**Original:** **Clean Markdown for AI agents.** Every page is also available as clean Markdown, with all the layout components resolved into plain text so AI assistants and tools get parseable content. There are three ways to get it:

**中文译文:** **为 AI agents 提供干净的 Markdown。** 每个页面都同时提供干净的 Markdown 版本，所有布局组件都会被解析为纯文本，使 AI 助手和其他工具能够直接解析内容。你可以通过以下 3 种方式获取：

**Original:**
- Use the **View as Markdown** option in the toolbar below the page title (in Elegant and AI modes).
- In **Markdown mode**, click the **View this page as .md** button next to that toolbar.
- Or go straight to the Markdown URL by adding `.md` to any page address, for example [docs.strapi.io/cms/api/rest.md](/cms/api/rest.md).

**中文译文:**
- 在 Elegant mode 或 AI mode 下，使用页面标题下方工具栏中的 **View as Markdown**。
- 在 **Markdown mode** 下，点击工具栏旁边的 **View this page as .md** 按钮。
- 也可以直接在任意页面地址末尾添加 `.md`，访问对应的 Markdown URL，例如 [docs.strapi.io/cms/api/rest.md](/cms/api/rest.md)。

**Original:** You can also point tools at the aggregated [llms.txt](/llms.txt), [llms-full.txt](/llms-full.txt), and [llms-code.txt](/llms-code.txt) files.

**中文译文:** 你还可以让工具直接读取聚合后的 [llms.txt](/llms.txt)、[llms-full.txt](/llms-full.txt) 和 [llms-code.txt](/llms-code.txt) 文件。

**Original:** **Page feedback widget.** Tell us what works and what does not, directly from the docs. You can leave general feedback using the widget at the bottom of each page, or select some text or code and click the floating **Leave feedback** button to send specific feedback about that content. Your input goes straight to the docs team.

**中文译文:** **页面反馈组件。** 你可以直接在文档中告诉我们哪些内容好用、哪些地方需要改进。既可以使用每个页面底部的组件提交整体反馈，也可以选中某段文字或代码，再点击浮动的 **Leave feedback** 按钮，针对选中内容发送具体反馈。你的意见会直接发送给文档团队。

**Original:** **Contribute with Inki, our docs plugin for Claude Code.** [Inki](https://github.com/strapi/documentation/tree/main/claude-plugins/inki) is a Claude Code plugin that bundles the skills, prompts, templates, and editorial rules the Strapi docs team uses to research, write, review, and submit documentation. It helps you find where new content belongs, draft it from the right template, check it against our style guide and verify code examples, then open a pull request. You can install it from this repository's marketplace and run the whole workflow, or any single step, from Claude Code.

**中文译文:** **使用 Inki 参与贡献——这是我们的 Claude Code 文档插件。** [Inki](https://github.com/strapi/documentation/tree/main/claude-plugins/inki) 是一个 Claude Code 插件，内置了 Strapi 文档团队在调研、撰写、审校和提交文档时使用的 skills、prompts、templates 与编辑规范。它可以帮助你判断新内容应该放在哪里，基于正确的模板起草文档，按照风格指南检查内容、验证代码示例，并最终创建 pull request。你可以从本仓库的 marketplace 安装 Inki，然后在 Claude Code 中运行完整工作流，也可以只执行其中某一个步骤。
