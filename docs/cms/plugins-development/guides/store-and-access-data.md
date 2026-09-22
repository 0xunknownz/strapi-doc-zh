# 📖 对照翻译：How to store and access data from a Strapi plugin

> Source: `docusaurus/docs/cms/plugins-development/guides/store-and-access-data.md`  
> Upstream SHA: `a936c1f45fc37db2034db453890a8d4ade9834c0`

**Original:** Store plugin data in plugin content-types, then use Document Service API or Query Engine API from the server.

**中文译文:** Plugin 持久化业务数据的标准方式是创建 **plugin content-type**。它与普通 Strapi content-type 一样拥有 schema、controller、service、route，并可通过 Document Service / Query Engine 操作。

## Generate a plugin content-type

**Original:** Run the generator from the plugin `server/src/` directory.

```bash
# Yarn
yarn strapi generate content-type

# NPM
npm run strapi generate content-type
```

**中文译文:** Interactive generator 中，在：

`Where do you want to add this model?`

选择：

`Add model to existing plugin`

再输入目标 plugin name。

**Original:** The generator creates schema plus basic controller/service/route code.

**中文译文:** Generator 通常会生成：
- Content-type schema；
- Basic controller；
- Service；
- Route。

## Admin visibility

**Original:** If a plugin content-type is not visible in Content Manager/Content-Type Builder, enable pluginOptions visibility.

```json
{
  "pluginOptions": {
    "content-manager": {
      "visible": true
    },
    "content-type-builder": {
      "visible": true
    }
  }
}
```

## Ensure imports exist

**Original:** Verify the plugin server entry exports `contentTypes`.

**中文译文:** 某些 generator/version 组合可能没有把所有 files 自动 wire 起来，应确认：

```js
const contentTypes =
  require(
    './content-types'
  );

module.exports = {
  register,
  bootstrap,
  destroy,
  config,
  controllers,
  routes,
  services,
  contentTypes,
  policies,
  middlewares,
};
```

**Original:** Also ensure the content-type index exports its schema.

```js
const schema =
  require('./schema');

module.exports = {
  schema,
};
```

## Data access

**Original:** Plugin database data can only be accessed from the server side.

**中文译文:** `/admin` browser code 不能直接访问 database。需要修改 plugin data 时：
1. Server 创建 controller/route；
2. Admin 通过 authenticated fetch client 请求 server endpoint。

## Document Service API

```js
const data =
  await strapi
    .documents(
      'plugin::my-plugin.my-plugin-content-type'
    )
    .findMany();
```

**中文译文:** 推荐优先使用 Document Service API，尤其 content model 含 components、dynamic zones、Draft & Publish 等 Strapi 语义时。

## Query Engine API

```js
const data =
  await strapi.db
    .query(
      'plugin::my-plugin.my-plugin-content-type'
    )
    .findMany();
```

**中文译文:** Query Engine 适合确实需要 unrestricted low-level database access 的场景。

**Original:** The UID syntax is `plugin::<plugin-slug>.<content-type-key>`.

**中文译文:** Plugin content-type UID 使用：

`plugin::<plugin-slug>.<content-type-key>`

例如：

`plugin::my-plugin.my-plugin-content-type`
