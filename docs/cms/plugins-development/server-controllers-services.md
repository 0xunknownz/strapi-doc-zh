# 📖 对照翻译：Server API — Controllers & Services

> Source: `docusaurus/docs/cms/plugins-development/server-controllers-services.md`  
> Upstream SHA: `2e409b8eea507a441d9dc4a4f143a485ea47b96e`

**Original:** Controllers own the HTTP layer; services own reusable domain logic.

**中文译文:** Plugin server 推荐明确分层：
- Controller：处理 HTTP context、request、status、response；
- Service：封装可复用 business/domain logic、database access、external API interaction。

## Controllers

**Original:** A controller is a map of actions referenced by route handlers.

**中文译文:** Controller export key 必须与 route handler 中的 controller name 对应。例如 `handler: 'article.find'` 需要 controllers registry 中存在 `article.find`。

**Original:** Controllers may be factory functions receiving `{ strapi }` or plain objects; factory form is recommended.

**中文译文:** Strapi runtime 支持 factory export 与 plain object；推荐 factory form，便于 dependency injection 与保持文档示例一致。

```js
module.exports = ({ strapi }) => ({
  async find(ctx) {
    const articles = await strapi
      .plugin('my-plugin')
      .service('article')
      .findAll();

    ctx.body = articles;
  },

  async findOne(ctx) {
    const { documentId } = ctx.params;

    const article = await strapi
      .plugin('my-plugin')
      .service('article')
      .findOne(documentId);

    if (!article) {
      return ctx.notFound(
        'Article not found'
      );
    }

    ctx.body = article;
  },

  async create(ctx) {
    const article = await strapi
      .plugin('my-plugin')
      .service('article')
      .create(ctx.request.body);

    ctx.status = 201;
    ctx.body = article;
  },
});
```

## Sanitization

**Original:** Plugin controllers do not inherit `createCoreController` helpers, so use `strapi.contentAPI.sanitize` explicitly.

**中文译文:** Plugin controller 是普通 factory，不像 application core controller 那样自动拥有 `this.sanitizeQuery` / `this.sanitizeOutput`。对 Content API route 必须显式使用：

`strapi.contentAPI.sanitize.*`

```js
module.exports = ({ strapi }) => ({
  async find(ctx) {
    const schema =
      strapi.contentType(
        'plugin::my-plugin.article'
      );

    const sanitizedQuery =
      await strapi.contentAPI.sanitize.query(
        ctx.query,
        schema,
        {
          auth: ctx.state.auth,
        }
      );

    const articles = await strapi
      .plugin('my-plugin')
      .service('article')
      .findAll(sanitizedQuery);

    ctx.body =
      await strapi.contentAPI.sanitize.output(
        articles,
        schema,
        {
          auth: ctx.state.auth,
        }
      );
  },
});
```

**中文译文:** 这可以避免 private field 泄漏、非法 populate/filter 绕过 permission 等问题。

## Services

**Original:** Services hold reusable logic and normally call Document Service API.

**中文译文:** Service 推荐以 resource 为单位组织，并通过 Document Service API 操作 plugin content-type。

```js
module.exports = ({ strapi }) => ({
  async findAll(params = {}) {
    return strapi
      .documents(
        'plugin::my-plugin.article'
      )
      .findMany(params);
  },

  async findOne(documentId) {
    return strapi
      .documents(
        'plugin::my-plugin.article'
      )
      .findOne({
        documentId,
      });
  },

  async create(data) {
    return strapi
      .documents(
        'plugin::my-plugin.article'
      )
      .create({
        data,
      });
  },

  async update(documentId, data) {
    return strapi
      .documents(
        'plugin::my-plugin.article'
      )
      .update({
        documentId,
        data,
      });
  },

  async delete(documentId) {
    return strapi
      .documents(
        'plugin::my-plugin.article'
      )
      .delete({
        documentId,
      });
  },
});
```

## TypeScript service typing

**Original:** Plugin services are currently typed as `unknown` in the ServerObject interface.

**中文译文:** 当前 Strapi TypeScript ServerObject 对 plugin `services` 的类型仍较宽，`strapi.plugin('my-plugin').service('article')` 可能推断为 `unknown`。建议定义明确 service interface，并在调用点进行 narrow cast，而不是在整个 codebase 使用 `any`。

## End-to-end flow

**Original:** Route → Controller → Service → Document Service.

**中文译文:** 推荐的 request flow：

`HTTP Route → Plugin Controller → Plugin Service → Document Service → Database`

Controller 负责 HTTP orchestration，service 负责 domain/data logic。

## Best practices

**中文译文:**
- Controller 保持薄，只做 `ctx` 读取、service delegation、response 设置；
- 一个 resource 对应一个主要 service；
- Document Service 调用放 service，而不是散落 controller；
- Content API response 返回前执行 sanitization；
- TypeScript 中给 dynamic plugin service 做显式 interface cast。
