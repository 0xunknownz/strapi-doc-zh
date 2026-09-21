# 📖 对照翻译：Services

> Source: `docusaurus/docs/cms/backend-customization/services.md`  
> Upstream SHA: `ec4ebe2835eebe8ca61ca48bc951c6a7aaa5b099`

**Original:** Services store reusable functions to keep controllers concise and follow DRY principles. This documentation explains generating or extending services with `createCoreService` and organizing them for APIs or plugins.

**中文译文:** Service 用于存放可复用 function，让 controller 保持简洁并遵循 DRY（Don't Repeat Yourself）原则。本页介绍如何通过 `createCoreService` 创建、扩展或替换 core service，以及 API / plugin service 的组织方式。

**Original:** Services are reusable functions, especially useful for simplifying controller logic.

**中文译文:** Service 是可复用业务逻辑集合。复杂 controller 中重复出现的 database / integration / domain logic 通常应下沉到 service。

## Implementation

**Original:** Services can be generated/manually added. `createCoreService` generates core methods and lets you add, wrap, or replace them.

**中文译文:** Service 可以通过 CLI 生成或手动创建。`createCoreService` 会生成 content-type core service methods，同时允许：
1. 增加全新 method；
2. Wrap 现有 core method；
3. 完全替换某个 core method。

### Adding a new service

**Original:** Locations:
- `./src/api/[api-name]/services/` for API services
- `./src/plugins/[plugin-name]/services/` for plugin services

**中文译文:** 文件位置：
- API service：`./src/api/[api-name]/services/`；
- Plugin service：`./src/plugins/[plugin-name]/services/`。

**Original:** A service exports a factory that receives the `strapi` instance and returns an object of methods.

**中文译文:** 手动创建 service 时，export 一个 factory function；factory 接收 `strapi` instance，并返回包含 service methods 的 object。

**Original example (kept unchanged):**

```js
const { createCoreService } = require('@strapi/strapi').factories;

module.exports = createCoreService('api::restaurant.restaurant', ({ strapi }) => ({
  async exampleService(...args) {
    let response = { okay: true };

    if (response.okay === false) {
      return { response, error: true };
    }

    return response;
  },

  async find(...args) {
    const { results, pagination } = await super.find(...args);

    results.forEach(result => {
      result.counter = 1;
    });

    return { results, pagination };
  },

  async findOne(documentId, params = {}) {
    return strapi.documents('api::restaurant.restaurant').findOne({
      documentId,
      ...super.getFetchParams(params),
    });
  }
}));
```

**中文译文:** 示例展示 3 种模式：
- `exampleService()`：新增完全自定义 service method；
- Override `find()` 并调用 `super.find()`：保留 core behavior，再对结果增加 custom logic；
- Override `findOne()`：不调用 core fetch，而是直接使用 Document Service；同时借助 `super.getFetchParams()` 复用 core parameter formatting。

**Original:** Use Document Service API functions as building blocks for custom services.

**中文译文:** 编写自定义 service 时，优先以 [Document Service API](/cms/api/document-service) 作为数据访问层。

### Custom email service example

**Original:** A service can hold reusable integration logic, such as a Nodemailer `sendNewsletter()` function that can be called by controllers or other services.

**中文译文:** Service 也适合封装第三方 integration。例如可以集中实现 Nodemailer `sendNewsletter()`，供多个 controller / service 重复调用。

```js
const { createCoreService } = require('@strapi/strapi').factories;
const nodemailer = require('nodemailer');

const transporter = nodemailer.createTransport({
  service: 'Gmail',
  auth: {
    user: 'user@gmail.com',
    pass: 'password',
  },
});

module.exports = createCoreService('api::restaurant.restaurant', ({ strapi }) => ({
  sendNewsletter(from, to, subject, text) {
    return transporter.sendMail({ from, to, subject, text });
  },
}));
```

**中文译文:** 上例把 SMTP transporter 与发送逻辑封装到 restaurant service。实际 production 中不要硬编码 credentials，应使用 environment variables / secrets。

**Original:** Call an API service with `strapi.service('api::restaurant.restaurant').sendNewsletter(...args)`.

**中文译文:** 创建后，可在任意 controller 或其他 service 中通过：
`strapi.service('api::restaurant.restaurant').sendNewsletter(...args)`
调用。

**Original:** A newly created content type gets a generic service placeholder ready for customization.

**中文译文:** 创建新 content-type 后，Strapi 会为它生成 generic service 文件，可直接扩展。

## Extending core services

**Original:** Core services can be customized. Naming a custom method the same as a core method replaces that method.

**中文译文:** Core service method 可以 override。自定义 service 中定义与 core method 同名的 method（如 `find`、`findOne`、`create`、`update`、`delete`）即可替换 / wrap 默认实现。

### Collection type patterns

```js
async find(params) {
  const { results, pagination } = await super.find(params);
  return { results, pagination };
}

async findOne(documentId, params) {
  const result = await super.findOne(documentId, params);
  return result;
}

async create(params) {
  return super.create(params);
}

async update(documentId, params) {
  return super.update(documentId, params);
}

async delete(documentId, params) {
  return super.delete(documentId, params);
}
```

**中文译文:** Collection type core service 使用 `documentId` 作为 document identifier。通过 `super.*` 保留默认逻辑，然后可在调用前后添加 custom business logic。

### Single type patterns

```js
async find(params) {
  return super.find(params);
}

async createOrUpdate({ data, ...params }) {
  return super.createOrUpdate({ data, ...params });
}

async delete(params) {
  return super.delete(params);
}
```

**中文译文:** Single type 没有多个 document collection，因此 core API 使用 `find`、`createOrUpdate`、`delete` 等方法。

## Usage

**Original:** Access services through:
```js
strapi.service('api::apiName.serviceName').FunctionName();
strapi.service('plugin::pluginName.serviceName').FunctionName();
```

**中文译文:** API service 与 plugin service 分别使用 `api::` / `plugin::` UID 访问。可运行 `yarn strapi services:list` 查看全部可用 services。

## Core service methods

**Original — Collection types:**

| Method | Description |
|---|---|
| `find(params)` | Document Service `findMany` wrapper |
| `findOne(documentId, params)` | `findOne` wrapper |
| `create(params)` | `create` wrapper |
| `update(documentId, params)` | `update` wrapper |
| `delete(documentId, params)` | `delete` wrapper |
| `count(params)` | `count` wrapper |
| `publish(documentId, params)` | `publish` wrapper |
| `unpublish(documentId, params)` | `unpublish` wrapper |
| `discardDraft(documentId, params)` | `discardDraft` wrapper |

**中文译文:** Collection type 的 core service methods 主要是 Document Service API 的 wrapper，并增加 controller-friendly parameter handling 与默认行为。

**Original — Single types:**

| Method | Description |
|---|---|
| `find(params)` | Uses `findFirst` internally |
| `createOrUpdate({data,...params})` | Create/update single document |
| `delete(params)` | Delete document |
| `count(params)` | Count |
| `publish(params)` | Publish |
| `unpublish(params)` | Unpublish |
| `discardDraft(params)` | Discard draft |

**中文译文:** Single type core service 对应唯一 document，内部同样基于 Document Service 实现。

**Original:** Core service methods accept Document Service parameters such as `fields`, `filters`, `sort`, `pagination`, `populate`, `locale`, and `status`.

**中文译文:** Core service methods 接收与 Document Service 相同的常用 parameters：`fields`、`filters`、`sort`、`pagination`、`populate`、`locale`、`status` 等。

**Original:** Unlike raw Document Service, core services default to `status: 'published'` when status is omitted.

**中文译文:** 一个重要差异：raw Document Service 默认 draft，而 core service 在未提供 `status` 时会自动使用 `status: 'published'`，只返回 published content。若要查询 draft，需要显式传 `status: 'draft'`。

**Original:** `getFetchParams(params)` converts controller query objects to the parameter shape expected by service/Document Service calls.

**中文译文:** `createCoreService` 还提供 `getFetchParams(params)` helper，可将 controller query object 转换为 service / Document Service 需要的 parameter shape，适合 override core method 时复用。
