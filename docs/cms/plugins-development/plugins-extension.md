# 📖 对照翻译：Plugins extension

> Source: `docusaurus/docs/cms/plugins-development/plugins-extension.md`  
> Upstream SHA: `59729138248e345b9bc24ce9d94e2a954c6dd0dd`

**Original:** Existing plugins can be extended through `/src/extensions` or application lifecycle hooks.

**中文译文:** Strapi application 可以扩展已安装 plugin，主要方式：
- 在 `./src/extensions/<plugin-name>` 覆盖 content-type / server interface；
- 在 application `src/index.js|ts` 的 `register()` / `bootstrap()` 中通过 runtime getters 扩展。

**Original:** Plugin updates can break extensions; extensive customization may be better maintained as a fork.

**中文译文:** **Plugin extension 不属于稳定 public API contract。** Plugin upgrade、Strapi upgrade 都可能破坏 extension，而且 migration guide 通常不会覆盖这些自定义逻辑。定制非常深时应考虑 fork plugin。

**Original:** Admin-side plugin code currently requires patch-package for direct extension.

**中文译文:** Plugin admin panel 部分目前不能像 server 那样通过 `src/extensions` 完整覆盖；直接 patch 通常需要 `patch-package`，未来版本兼容风险较高。

## Extensions folder

```text
/src/extensions/
  /some-plugin/
    strapi-server.js|ts
    /content-types/
      /some-content-type/
        schema.json
```

## Extending plugin content-types

**Original:** Final schema loading order is original plugin → extension schema.json → extension `contentTypes` export → application `register()`.

**中文译文:** Plugin content-type final schema 的覆盖顺序：

1. 原 plugin content-type；
2. `src/extensions/<plugin>/content-types/.../schema.json`；
3. Extension `strapi-server.js|ts` 中的 `contentTypes` export；
4. Application `src/index.js|ts` 的 `register()`。

后面的声明可以继续覆盖前面的结果。

## Extending server interface

**Original:** Extension loading happens after plugins are loaded but before application register/bootstrap.

**中文译文:** Initialization 顺序：
1. Plugins 加载并暴露 interface；
2. `src/extensions` 被应用；
3. Application `register()` / `bootstrap()` 执行。

### Example

```js
module.exports = (plugin) => {
  plugin
    .controllers
    .controllerA
    .find =
      (ctx) => {};

  plugin.policies[
    'newPolicy'
  ] =
    (ctx) => {};

  plugin.routes[
    'content-api'
  ].routes.push({
    method: 'GET',
    path: '/route-path',
    handler:
      'controller.action',
  });

  return plugin;
};
```

**中文译文:** Extension function 接收原 plugin interface，修改后必须 return。

## Factory-based controller caveat

**Original:** Factory controllers cannot be overridden by assigning directly to an action before the factory is resolved.

**中文译文:** 某些 plugin controller（例如 Users & Permissions auth controller）本身是：

`({ strapi }) => ({ ...actions })`

这种 factory。Extension 执行时 action object 尚未创建，所以：

`plugin.controllers.auth.callback = ...`

不会按预期工作。

**Original:** Wrap the controller factory itself.

```js
module.exports = (plugin) => {
  const originalAuthFactory =
    plugin.controllers.auth;

  plugin.controllers.auth =
    ({ strapi }) => {
      const originalAuth =
        originalAuthFactory({
          strapi,
        });

      const originalCallback =
        originalAuth.callback;

      originalAuth.callback =
        async (ctx) => {
          // custom pre logic

          await originalCallback(
            ctx
          );

          // custom post logic
        };

      return originalAuth;
    };

  return plugin;
};
```

## Internal Upload extension

**Original:** Internal Upload services can be overridden, but these extension points are not stable.

**中文译文:** 例如可以覆盖 Upload plugin 的 `image-manipulation` internal service 来自定义文件命名，但这属于内部实现，不是稳定 public API，upgrade 风险较高。

## Application lifecycle extension

```js
module.exports = {
  register({
    strapi,
  }) {
    const contentType =
      strapi.contentType(
        'plugin::my-plugin.content-type-name'
      );

    contentType.attributes = {
      ...contentType.attributes,

      toto: {
        type: 'string',
      },
    };
  },
};
```

**中文译文:** Application-level `register()` 也可以通过 getter 取得 plugin content-type schema 并继续扩展。
