# 📖 对照翻译：Server API — Lifecycle

> Source: `docusaurus/docs/cms/plugins-development/server-lifecycle.md`  
> Upstream SHA: `22cd0a3fe349f4d7d85f3eb6dd20d1d13cc64602`

**Original:** The Server API has 3 lifecycle functions: `register()`, `bootstrap()`, and `destroy()`.

**中文译文:** Plugin Server API 有 3 个核心 lifecycle function：
- `register()`：Strapi 尚未完整初始化时注册能力；
- `bootstrap()`：Strapi 完整初始化后执行 runtime setup；
- `destroy()`：shutdown 时释放资源。

每个 function 都接收 `{ strapi }`。

## Startup sequence

| 阶段 | 可用能力 |
|---|---|
| Register | `strapi` object 已存在，但 database 与 routing 尚未完整初始化 |
| Bootstrap | Database、routes、services、content-types、其他 plugins 均可用 |
| Shutdown | 用于关闭连接、timer、listener 等资源 |

**Original:** Each lifecycle is called once per plugin instance.

**中文译文:** 正常运行中，每个 lifecycle 对每个 plugin instance 只调用一次。如果测试代码手工对同一 instance 重复调用，Strapi 会抛出 error。

## `register()`

**Original:** Runs before database and route initialization.

**中文译文:** `register()` 适合：
- 注册 custom field 的 server part；
- 注册 database migration；
- 通过 `strapi.server.use()` 注册 server middleware；
- 在 bootstrap 前扩展其他 plugin 的 content-type / interface。

```js title="/src/plugins/my-plugin/server/src/register.js"
'use strict';

module.exports = ({ strapi }) => {
  strapi.server.use(async (ctx, next) => {
    ctx.set('X-Plugin-Version', '1.0.0');
    await next();
  });
};
```

**Original:** Keep `register()` lightweight and avoid database reads/writes.

**中文译文:** `register()` 阶段 database 还没有初始化完成，因此不要在这里调用 `strapi.documents()` 或依赖 database 的 service。

## `bootstrap()`

**Original:** Runs after database, routes, permissions, services, and plugins are initialized.

**中文译文:** `bootstrap()` 适合：
- Seed initial data；
- 注册 admin RBAC actions；
- 注册 cron jobs；
- Subscribe database lifecycle events；
- 调用本 plugin / 其他 plugin services；
- 建立依赖其他 plugin 已完成初始化的 integration。

```js title="/src/plugins/my-plugin/server/src/bootstrap.js"
'use strict';

module.exports = async ({ strapi }) => {
  await strapi
    .service('admin::permission')
    .actionProvider
    .registerMany([
      {
        section: 'plugins',
        displayName: 'Read',
        uid: 'read',
        pluginName: 'my-plugin',
      },
      {
        section: 'plugins',
        displayName: 'Settings',
        uid: 'settings',
        pluginName: 'my-plugin',
      },
    ]);
};
```

**中文译文:** Admin RBAC action 应在 `bootstrap()` 注册，因为此时 permission service 已可用。

## `destroy()`

**Original:** Runs during shutdown and is optional.

**中文译文:** 只有 plugin 持有需要显式释放的资源时才需要实现 `destroy()`，例如：
- External database / message queue connection；
- WebSocket server；
- `setInterval` / `setTimeout`；
- Process / event listener。

```js title="/src/plugins/my-plugin/server/src/destroy.js"
'use strict';

module.exports = ({ strapi }) => {
  strapi
    .plugin('my-plugin')
    .service('queue')
    .disconnect();
};
```

## Best practices

**中文译文:**
- `register()` 保持轻量，不做 DB I/O；
- Database reads/writes 放在 `bootstrap()`；
- 在 `bootstrap()` 注册 admin RBAC actions；
- 创建长期资源时同时实现 `destroy()`；
- `register()` 阶段避免依赖其他 plugin 已完成初始化；
- 复杂 lifecycle logic 下沉到 service，提高可测试性与可复用性。
