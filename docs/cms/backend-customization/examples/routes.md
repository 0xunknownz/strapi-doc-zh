# 📖 对照翻译：Examples cookbook — Custom routes

> Source: `docusaurus/docs/cms/backend-customization/examples/routes.md`  
> Upstream SHA: `c31ed7fc1e4c5c90ef07944dd22bf194b28d0171`

**Original:** Custom routes let you explicitly configure routes for content-types to control authentication and apply policies, such as bypassing default Strapi authentication or restricting access based on custom conditions.

**中文译文:** Custom route 可以显式覆盖 content-type route configuration，用于控制 authentication、policies 与 middlewares。例如，可以关闭默认 Strapi authentication，再使用 custom policy 实现更细粒度的访问规则。

## Context

**Original:** FoodAdvisor does not control access to content-type endpoints by default. Assume a custom policy was previously created to prevent restaurant owners from reviewing their own restaurant.

**中文译文:** FoodAdvisor 默认没有针对 content-type endpoint 的 custom access control。假设上一节已经创建 `is-owner-review` policy，用来阻止 restaurant owner 为自己的 restaurant 创建 review；现在需要把该 policy 真正绑定到 route。

## Goals

**Original:**
- Explicitly define route configuration for Reviews.
- Configure the create route to bypass default authentication.
- Apply the custom policy.

**中文译文:** 目标：
- 为 Reviews content-type 显式定义 route configuration；
- 让 create route 跳过 Strapi 默认 authentication；
- 在该 route 上执行此前创建的 custom policy。

## Code example

**Original code (kept unchanged):**

```js title="src/api/review/routes/review.js"
'use strict';

const { createCoreRouter } = require('@strapi/strapi').factories;

module.exports = createCoreRouter('api::review.review', {
  config: {
    create: {
      auth: false,
      policies: ['is-owner-review'],
      middlewares: [],
    },
  },
});
```

**中文译文:** 关键配置：
- `auth: false`：关闭该 route 的默认 Strapi authentication gate；
- `policies: ['is-owner-review']`：在 controller 前执行 custom policy；
- `middlewares: []`：当前 route 没有额外 route middleware。

注意：`auth: false` 并不等于“没有任何安全控制”；本示例把访问判断交给 `is-owner-review` policy。实际项目应确保 policy 自己正确验证 `ctx.state.user` 或其他 credentials。

**Original:** Next, learn how to configure custom middlewares.

**中文译文:** 下一步参阅 [Custom middlewares](/cms/backend-customization/examples/middlewares)。
