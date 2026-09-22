# 📖 对照翻译：Server API for plugins — Overview

> Source: `docusaurus/docs/cms/plugins-development/server-api.md`  
> Upstream SHA: `373d194262216d93d627984dd948da484f9ed599`

**Original:** The Server API defines what a plugin registers, exposes, and executes on the Strapi server. It covers lifecycle hooks, routes, controllers, services, policies, middlewares, and configuration.

**中文译文:** Server API 定义 Strapi plugin 在 back-end server 中注册、暴露和执行的能力，包括 lifecycle hooks、configuration、content-types、routes、controllers、services、policies 与 middlewares。

**Original:** The server part is defined by an entry file that exports an object, or a function returning an object.

**中文译文:** Plugin server part 由 entry file 定义。Entry file 可以直接 export object，也可以 export 一个返回相同 object shape 的 function。

## Entry file

**Original:** The Server API entry file is `[plugin-name]/server/src/index.js|ts`.

**中文译文:** Server API 的默认 entry file 为：

`[plugin-name]/server/src/index.js|ts`

可导出的能力如下：

| 类型 | 可用能力 |
|---|---|
| Lifecycle | `register()`、`bootstrap()`、`destroy()` |
| Configuration | `config` |
| Backend customization | `contentTypes`、`routes`、`controllers`、`services`、`policies`、`middlewares` |

**Original code (kept unchanged):**

```js title="/src/plugins/my-plugin/server/src/index.js"
'use strict';

const register = require('./register');
const bootstrap = require('./bootstrap');
const destroy = require('./destroy');
const config = require('./config');
const contentTypes = require('./content-types');
const routes = require('./routes');
const controllers = require('./controllers');
const services = require('./services');
const policies = require('./policies');
const middlewares = require('./middlewares');

module.exports = () => ({
  register,
  bootstrap,
  destroy,
  config,
  contentTypes,
  routes,
  controllers,
  services,
  policies,
  middlewares,
});
```

```ts title="/src/plugins/my-plugin/server/src/index.ts"
import register from './register';
import bootstrap from './bootstrap';
import destroy from './destroy';
import config from './config';
import contentTypes from './content-types';
import routes from './routes';
import controllers from './controllers';
import services from './services';
import policies from './policies';
import middlewares from './middlewares';

export default () => ({
  register,
  bootstrap,
  destroy,
  config,
  contentTypes,
  routes,
  controllers,
  services,
  policies,
  middlewares,
});
```

**中文译文:** 技术上所有 server code 都可以放进这个 entry file，但强烈建议按照 Plugin SDK 生成的结构把不同 concern 拆分到独立目录，便于维护与测试。

**Original:** If the entry file exports a function, Strapi calls it with `{ env }`, not `{ strapi }`, while loading the plugin module.

**中文译文:** 如果 entry file 使用 function form，Strapi 在加载 plugin module 时传入的是 `{ env }`，**不是** `{ strapi }`。真正需要 `strapi` instance 的 logic 应放到 lifecycle、controller、service 等 runtime function 中。

**Original:** `config` is configuration data, not a lifecycle function.

**中文译文:** `config` 是 configuration object，而不是可执行的 lifecycle hook。它在 startup 时被加载、与用户配置合并并验证，不会像 `register()` / `bootstrap()` / `destroy()` 那样按生命周期调用。

## Available actions

| 目标 | 使用能力 | 执行阶段 |
|---|---|---|
| Server 完整初始化前注册能力 | `register()` | Database / routing 初始化前 |
| Plugins 全部加载后执行逻辑 | `bootstrap()` | Database / routes / permissions 初始化后 |
| Shutdown 时清理资源 | `destroy()` | Strapi shutdown |
| 定义 plugin defaults / validation | `config` | Startup |
| 定义 plugin content-types | `contentTypes` | Startup |
| 暴露 HTTP endpoints | `routes` | Startup |
| 处理 HTTP request | `controllers` | Per request |
| 封装业务逻辑 | `services` | Controller / lifecycle 调用时 |
| Route authorization | `policies` | Controller 前 |
| 拦截 request/response flow | `middlewares` | Route / server middleware chain |
| Runtime 获取 plugin resources | Getters | Lifecycle / request handler 中 |

**Original:** Plugin backend resources follow the same conventions as normal Strapi backend customization and are automatically namespaced by the plugin.

**中文译文:** Plugin 的 routes、controllers、services、policies、middlewares 与普通 Strapi [backend customization](/cms/backend-customization) 使用相同的基本约定，但 Strapi 会自动把它们注册到 plugin namespace 下。
