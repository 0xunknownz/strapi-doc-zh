# 📖 对照翻译：Server API — Getters & usage

> Source: `docusaurus/docs/cms/plugins-development/server-getters-usage.md`  
> Upstream SHA: `39045a6a4f93627172a4deb1ce682883857ed3ec`

**Original:** Plugin resources can be accessed through top-level plugin getters or global getters. Both return the same underlying object.

**中文译文:** Plugin 的 service、controller、content-type、policy、middleware 等资源可以通过两类 getter 获取：
- **Top-level plugin getter**：`strapi.plugin('todo').service('task')`
- **Global getter**：`strapi.service('plugin::todo.task')`

两种方式返回同一个 underlying object。

## Which style to use

**Original:** Prefer top-level getters inside the plugin and global getters from application code or another plugin.

**中文译文:**
- Plugin 自己内部：优先 `strapi.plugin('my-plugin').service('x')`，更直观；
- Application code / 其他 plugin：优先 full UID global getter，使跨 plugin dependency 更明确。

**Original:** Routes have no global getter, and configuration uses dedicated config APIs.

**中文译文:** 两个例外：
- Routes 只有 `strapi.plugin('name').routes`，没有 global equivalent；
- Configuration 使用 `plugin().config()` / `strapi.config.get()`，不是普通 resource getter。

## Full reference

| Resource | Top-level | Global |
|---|---|---|
| Service | `strapi.plugin('todo').service('task')` | `strapi.service('plugin::todo.task')` |
| Controller | `strapi.plugin('todo').controller('task')` | `strapi.controller('plugin::todo.task')` |
| Content-type | `strapi.plugin('todo').contentType('task')` | `strapi.contentType('plugin::todo.task')` |
| Policy | `strapi.plugin('todo').policy('is-owner')` | `strapi.policy('plugin::todo.is-owner')` |
| Middleware | `strapi.plugin('todo').middleware('audit-log')` | `strapi.middleware('plugin::todo.audit-log')` |
| Routes | `strapi.plugin('todo').routes` | — |
| Config | `strapi.plugin('todo').config('featureFlag')` | `strapi.config.get('plugin::todo.featureFlag')` |

## Service from a controller

```js
module.exports = ({ strapi }) => ({
  async find(ctx) {
    const tasks = await strapi
      .plugin('todo')
      .service('task')
      .findAll();

    ctx.body = tasks;
  },
});
```

**中文译文:** 在 plugin controller 内调用同 plugin service 时，top-level getter 最简洁。

## Service from bootstrap

```js
module.exports = async ({ strapi }) => {
  const taskService =
    strapi.plugin('todo').service('task');

  const count = await taskService.count();

  if (count === 0) {
    await taskService.create({
      title: 'Welcome task',
      done: false,
    });
  }
};
```

**中文译文:** `bootstrap()` 中可以访问完整 Strapi runtime，包括 plugin services 与其他 plugin resources。

## Cross-plugin/application call

```js
await strapi
  .service('plugin::todo.task')
  .create({
    title: 'Review project',
    done: false,
  });
```

**中文译文:** 跨 plugin / application 代码中使用 full UID，更容易看出 dependency 来源。

## Runtime configuration

```js
const maxItems =
  strapi.plugin('todo').config('maxItems');

const todoConfig =
  strapi.config.get('plugin::todo');

const endpoint =
  strapi.config.get('plugin::todo.endpoint');
```

**中文译文:** 这里读取的是 defaults 与用户 `config/plugins` overrides 合并后的最终配置。

## Common errors

**中文译文:**
- Route `handler: 'task.find'` 与 controllers registry key / method name 不匹配；
- 把 policyContext 当作原始 Koa `ctx` 使用；
- 在 module top-level 调 getter，此时 `strapi` 尚未初始化；
- Global getter 使用不完整 UID，例如 `todo.task`，正确应为 `plugin::todo.task`。

## Best practices

**中文译文:**
- Plugin 内部优先 top-level getter；
- 跨 plugin / application code 优先 global full UID；
- Getter 应在 function execution time 调用，不要在 module declaration 阶段缓存 service reference。
