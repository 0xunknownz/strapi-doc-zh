# 📖 对照翻译：How to populate creator fields such as `createdBy` and `updatedBy`

> Source: `docusaurus/docs/cms/api/rest/guides/populate-creator-fields.md`  
> Upstream SHA: `df9ac3585bbfda7d61ed2fe2c81498feb2135c4b`

**Original:** Enable the `populateCreatorFields` option in a content-type schema and create a route middleware to include `createdBy` and `updatedBy` fields in REST API responses.

**中文译文:** 在 content-type schema 中启用 `populateCreatorFields`，并创建 route middleware，即可让 REST API response 返回 `createdBy` 和 `updatedBy`。

**Original:** The creator fields `createdBy` and `updatedBy` are removed from REST API responses by default. They can be returned by activating `populateCreatorFields` at content-type level.

**中文译文:** 默认情况下，REST API response 会移除 creator fields `createdBy` 与 `updatedBy`。可以在 content-type level 启用 `populateCreatorFields`，允许 population 这些字段。

**Original:** `populateCreatorFields` is not available to GraphQL API. Only `id`, `firstname`, `lastname`, `username`, `preferedLanguage`, `createdAt`, and `updatedAt` are populated.

**中文译文:** `populateCreatorFields` **不适用于 GraphQL API**。Creator data 只会返回 `id`、`firstname`、`lastname`、`username`、`preferedLanguage`、`createdAt` 和 `updatedAt`。

**Original:** 1. Open the content-type `schema.json`.
2. Add `"populateCreatorFields": true` to `options`.

```json
"options": {
  "draftAndPublish": true,
  "populateCreatorFields": true
},
```

**中文译文:** 1. 打开目标 content-type 的 `schema.json`；
2. 在 `options` object 中添加 `"populateCreatorFields": true`。代码保持原样。

**Original:** 3. Save `schema.json`.
4. Create a route middleware using the CLI or manually under `./src/api/[content-type-name]/middlewares/[your-middleware-name].js`.

**中文译文:** 3. 保存 `schema.json`；
4. 使用 Strapi generate CLI 创建 route middleware，或手动创建 `./src/api/[content-type-name]/middlewares/[your-middleware-name].js`。

**Original code (kept unchanged):**

```js title="./src/api/test/middlewares/defaultTestPopulate.js"
"use strict";

module.exports = (config, { strapi }) => {
  return async (ctx, next) => {
    if (!ctx.query.populate) {
      ctx.query.populate = ["createdBy", "updatedBy"];
    }

    await next();
  };
};
```

**中文译文:** 该 middleware 会在 request 未显式传入 `populate` 时，自动把 `createdBy` 与 `updatedBy` 加入 population。

**Original:** 6. Enable the middleware on the routes you want by modifying the default route factory.

**中文译文:** 6. 修改默认 route factory，把 middleware 加到需要应用 creator population 的 routes。

```js title="./src/api/test/routes/test.js"
"use strict";

const { createCoreRouter } = require("@strapi/strapi").factories;

module.exports = createCoreRouter("api::test.test", {
  config: {
    find: {
      middlewares: ["api::test.default-test-populate"],
    },
    findOne: {
      middlewares: ["api::test.default-test-populate"],
    },
  },
});
```

**中文译文:** 上例对 `find` 和 `findOne` 启用该 middleware。请将 content-type UID 与 middleware name 替换为项目实际名称。

**Original:** REST requests with no `populate` parameter will then include `createdBy` and `updatedBy` by default.

**中文译文:** 配置完成后，没有显式 `populate` parameter 的 REST request 会默认返回 `createdBy` / `updatedBy`。
