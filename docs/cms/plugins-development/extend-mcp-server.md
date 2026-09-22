# 📖 对照翻译：Extending the MCP server with plugins

> Source: `docusaurus/docs/cms/plugins-development/extend-mcp-server.md`  
> Upstream SHA: `c6907b24c1fd4df08f45f5404f4548de9490e69a`

**Original:** Plugins can register MCP tools, resources, and prompts through `strapi.ai.mcp`.

**中文译文:** Strapi plugin 可以通过 `strapi.ai.mcp` 扩展 built-in MCP server，为 AI client 注册 plugin-specific：
- Tool；
- Resource；
- Prompt。

**Original:** Registrations must happen during `register()`, while the MCP server is still idle.

**中文译文:** **必须在 plugin `register()` lifecycle 注册 MCP capability。** MCP server 启动后不能再安全添加这些定义。

## Register a tool

```js
const {
  z,
} = require('@strapi/utils');

module.exports = {
  register({
    strapi,
  }) {
    strapi.ai.mcp.registerTool({
      name: 'my_custom_tool',
      title: 'My Custom Tool',
      description:
        'A short description shown to the AI client.',

      auth: {
        policies: [
          {
            action:
              'plugin::my-plugin.my-action',
          },
        ],
      },

      resolveInputSchema:
        () =>
          z.object({
            message:
              z.string(),
          }),

      resolveOutputSchema:
        () =>
          z.object({
            result:
              z.string(),
          }),

      createHandler:
        (strapi, context) =>
          async ({ args }) => ({
            content: [
              {
                type: 'text',
                text: args.message,
              },
            ],
            structuredContent: {
              result:
                args.message,
            },
          }),
    });
  },
};
```

## Tool options

| Option | Required | 中文说明 |
|---|---:|---|
| `name` | Yes | 全局唯一 tool name |
| `title` | Yes | AI client 展示的人类可读标题 |
| `description` | Yes | Tool 用途说明 |
| `auth` | 二选一 | Admin-token permission policies；任一 policy 满足即可 |
| `devModeOnly` | 二选一 | 只在 development mode 可用 |
| `resolveInputSchema` | No | 每个 request 动态生成 Zod input schema |
| `resolveOutputSchema` | Yes | 每个 request 动态生成 structured output schema |
| `createHandler` | Yes | 创建实际 async handler |

**Original:** Input/output schema resolvers run per request, so they can use `context.userAbility` to narrow schemas dynamically.

**中文译文:** Schema resolver 每个 MCP request 都会执行，因此可以根据 `context.userAbility` 动态限制可操作 fields / actions，实现 permission-aware tool schema。

## Builder helpers

**Original:** `ai.mcp.defineTool`, `defineResource`, and `definePrompt` are optional TypeScript inference helpers.

**中文译文:** 对大型 TypeScript plugin，可以把 capability 定义拆到独立 module，并使用：
- `ai.mcp.defineTool`
- `ai.mcp.defineResource`
- `ai.mcp.definePrompt`

它们只是 **identity/type-inference helpers**，不会自动注册 capability。

### Tool

```ts
import {
  ai,
} from '@strapi/strapi';

import {
  z,
} from '@strapi/utils';

export const greet =
  ai.mcp.defineTool({
    name: 'greet',
    title: 'Greet',
    description:
      'Greets a user by name',
    devModeOnly: true,

    resolveInputSchema:
      () =>
        z.object({
          name: z.string(),
        }),

    resolveOutputSchema:
      () =>
        z.object({
          message:
            z.string(),
        }),

    createHandler:
      () =>
        async ({ args }) => {
          const message =
            `Hello, ${args.name}!`;

          return {
            content: [
              {
                type: 'text',
                text: message,
              },
            ],
            structuredContent: {
              message,
            },
          };
        },
  });
```

**中文译文:** 定义之后仍需在 `register()` 中：

`strapi.ai.mcp.registerTool(greet)`

## Resources

**Original:** Resources expose read-only data through a URI.

**中文译文:** Resource 用稳定 URI 暴露 read-only data，例如 `strapi://app/info`，通过 `registerResource()` 注册。

## Prompts

**Original:** Prompts expose reusable prompt templates to MCP clients.

**中文译文:** Prompt 用于向 AI client 提供可复用 prompt template，通过 `registerPrompt()` 注册。

**Original:** A capability must choose either `devModeOnly: true` or `auth`, never both.

**中文译文:** 每个 capability 必须在：
- `devModeOnly: true`
- `auth: {...}`

之间二选一，不能同时使用。
