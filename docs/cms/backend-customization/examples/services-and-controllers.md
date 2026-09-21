# 📖 对照翻译：Examples cookbook — Custom services and controllers

> Source: `docusaurus/docs/cms/backend-customization/examples/services-and-controllers.md`  
> Upstream SHA: `7972e07d3eefe090879fe842343569874390e2b9`

**Original:** Services encapsulate reusable business logic that controllers invoke to handle reviews and email notifications. This guide demonstrates creating custom services using the Document Service API and custom controllers that call them.

**中文译文:** Service 用于封装可复用 business logic，controller 则负责接收 HTTP request 并编排这些 service。本指南通过“创建 review + 给 restaurant owner 发送 email”的完整示例，展示 Document Service、custom service 与 custom controller 如何协同。

## REST API queries from the front end

**Original:** FoodAdvisor restaurant pages originally display reviews in read-only mode. The example adds a form so users can submit reviews directly from the front-end website.

**中文译文:** FoodAdvisor 的 restaurant page 默认只能读取 reviews。本示例在 Next.js front end 中增加一个 review form，让用户直接从页面向 Strapi REST API 提交 review。

**Original:** Goals:
- Add a review form.
- Display it on restaurant pages.
- POST to the REST API.
- Authenticate using the previously stored JWT.

**中文译文:** 目标：
- 新增 review form；
- 将 form 显示在 restaurant page；
- 提交时向 Strapi REST API 发送 `POST`；
- 使用之前保存在 `localStorage` 中的 JWT authentication request。

**Original code (kept unchanged):**

```jsx title="/client/components/pages/restaurant/RestaurantContent/Reviews/new-review.js"
import { Button, Input, Textarea } from '@nextui-org/react';
import { useFormik } from 'formik';
import { useRouter } from 'next/router';
import React from 'react';
import { getStrapiURL } from '../../../../../utils';

const NewReview = () => {
  const router = useRouter();

  const { handleSubmit, handleChange, values } = useFormik({
    initialValues: {
      note: '',
      content: '',
    },
    onSubmit: async (values) => {
      const res = await fetch(getStrapiURL('/reviews'), {
        method: 'POST',
        body: JSON.stringify({
          restaurant: router.query.slug,
          ...values,
        }),
        headers: {
          Authorization: `Bearer ${localStorage.getItem('token')}`,
          'Content-Type': 'application/json',
        },
      });
    },
  });

  return (
    <div className="my-6">
      <h1 className="font-bold text-2xl mb-3">Write your review</h1>
      <form onSubmit={handleSubmit} className="flex flex-col gap-y-4">
        <Input
          onChange={handleChange}
          name="note"
          type="number"
          min={1}
          max={5}
          label="Stars"
        />
        <Textarea
          name="content"
          onChange={handleChange}
          placeholder="What do you think about this restaurant?"
        />
        <Button
          type="submit"
          className="bg-primary text-white rounded-md self-start"
        >
          Send
        </Button>
      </form>
    </div>
  );
};

export default NewReview;
```

**中文译文:** Front-end 核心逻辑保持原样：
- restaurant slug 来自 `router.query.slug`；
- form values 中包含 rating / review content；
- request 使用 `Authorization: Bearer <jwt>`；
- POST target 为 `/reviews`。

**Original:** Add `<NewReview />` to the Reviews component to display the form on restaurant pages.

**中文译文:** 然后在 restaurant 的 Reviews component 中 import `NewReview` 并渲染 `<NewReview />`，即可让每个 restaurant page 显示该表单。

## Controllers vs. Services

**Original:** Controllers can contain business logic, but as code grows it is best practice to move reusable, single-purpose logic into services and let controllers orchestrate them.

**中文译文:** Controller 可以直接包含 business logic，但随着项目增长，最佳实践是把可复用、职责单一的逻辑拆到 service，再由 controller 负责 orchestration。这样能减少重复代码，并降低 controller 复杂度。

**Original:** In this guide the controller delegates all business logic to services:
1. create a review,
2. send an email,
3. customize the Review controller to invoke both.

**中文译文:** 本示例将业务逻辑拆成 3 步：
1. Custom review service：创建 review；
2. Custom email service：发送 notification；
3. Custom Review controller：调用前两个 services，并返回 sanitized response。

## Custom service: Creating a review

**Original:** The custom `create(ctx)` service reads request context, finds the restaurant with Document Service, creates a review, connects it to the restaurant and authenticated user, populates the restaurant owner, and returns the new review.

**中文译文:** 自定义 `create(ctx)` service：
- 从 `ctx.state.user` 获取 authenticated user；
- 从 `ctx.request.body` 获取 review payload；
- 使用 Document Service 查找 restaurant；
- 创建新的 Review document；
- 连接 restaurant 与 author；
- populate `restaurant.owner`；
- 返回新 review。

**Original code (kept unchanged):**

```js title="src/api/review/services/review.js"
const { createCoreService } = require('@strapi/strapi').factories;

module.exports = createCoreService('api::review.review', ({ strapi }) => ({
  async create(ctx) {
    const user = ctx.state.user;
    const { body } = ctx.request;

    const restaurants = await strapi.documents('api::restaurant.restaurant').findMany({
      filters: {
        slug: body.restaurant,
      },
    });

    const newReview = await strapi.documents('api::review.review').create({
      data: {
        note: body.note,
        content: body.content,
        restaurant: restaurants[0].documentId,
        author: user.id,
      },
      populate: ['restaurant.owner'],
    });

    return newReview;
  },
}));
```

**中文译文:** 这里直接使用 Document Service API，而不是低层 Query Engine。Restaurant relation 使用 `documentId`，author 则依据实际 Users & Permissions relation schema 写入当前 user。示例未包含 restaurant 不存在等 error handling；production code 应补充 validation 与错误处理。

**Original:** The service can be called with `strapi.service('api::review.review').create(ctx)`.

**中文译文:** Controller 中通过 `strapi.service('api::review.review').create(ctx)` 调用该 service。

## Custom service: Sending an email to the restaurant owner

**Original:** This optional example uses the Email plugin and a configured provider. It reads the sender address from an Email single type and sends a message through the Email plugin.

**中文译文:** 该高级示例是可选部分，依赖 Strapi Email plugin 与已配置的 email provider。Sender address 存放在一个 Email single type 中，service 读取配置后通过 Email plugin 发信。

**Original:** Prerequisites:
- Configure an Email provider.
- Create an Email single type with a `from` Text field.

**中文译文:** 前置条件：
- 已配置 [Email provider](/cms/features/email)；
- 在 admin panel 创建 `Email` single type，并添加 `from` Text field 保存 sender address。

**Original code (kept unchanged):**

```js title="src/api/email/services/email.js"
const { createCoreService } = require('@strapi/strapi').factories;

module.exports = createCoreService('api::email.email', ({ strapi }) => ({
  async send({ to, subject, html }) {
    const emailConfig = await strapi.documents('api::email.email').findFirst();

    await strapi.plugins['email'].services.email.send({
      to,
      subject,
      html,
      from: emailConfig.from,
    });
  },
}));
```

**中文译文:** Single type 通过 Document Service `findFirst()` 取得唯一 document；随后调用 Email plugin 的 `services.email.send()`。调用方只需传 `to`、`subject`、`html`。

**Original:** The service can be called with `strapi.service('api::email.email').send(parameters)`.

**中文译文:** Controller / service 中可通过 `strapi.service('api::email.email').send(parameters)` 复用该逻辑。

## Custom controller

**Original:** The default Review core controller can be overridden by defining a custom `create()` action with the same name.

**中文译文:** 使用 `createCoreController` 时，如果定义与 core action 同名的 `create()`，就会 override 默认 Review create action。

### Controller without email service

**Original code (kept unchanged):**

```js title="src/api/review/controllers/review.js"
const { createCoreController } = require('@strapi/strapi').factories;

module.exports = createCoreController('api::review.review', ({ strapi }) => ({
  async create(ctx) {
    const newReview = await strapi.service('api::review.review').create(ctx);

    const sanitizedReview = await this.sanitizeOutput(newReview, ctx);

    ctx.body = sanitizedReview;
  },
}));
```

**中文译文:** Controller 不直接实现 create business logic，而是调用 review service。返回 response 前使用 `this.sanitizeOutput(newReview, ctx)` 清理输出，避免泄露当前 caller 无权看到的 fields。

### Controller with email service

**Original code (kept unchanged):**

```js title="src/api/review/controllers/review.js"
const { createCoreController } = require('@strapi/strapi').factories;

module.exports = createCoreController('api::review.review', ({ strapi }) => ({
  async create(ctx) {
    const newReview = await strapi.service('api::review.review').create(ctx);

    if (newReview.restaurant?.owner) {
      await strapi.service('api::email.email').send({
        to: newReview.restaurant.owner.email,
        subject: 'You have a new review!',
        html: `You've received a ${newReview.note} star review: ${newReview.content}`,
      });
    }

    const sanitizedReview = await this.sanitizeOutput(newReview, ctx);

    ctx.body = sanitizedReview;
  },
}));
```

**中文译文:** 扩展版本在 review 创建后检查 `newReview.restaurant?.owner`；存在 owner 时调用 email service 发送 notification，然后仍然通过 `sanitizeOutput` 返回安全 response。

**Original:** Next, learn how custom policies can restrict access based on specific conditions.

**中文译文:** 下一步可继续阅读 [Custom policies](/cms/backend-customization/examples/policies)，在 controller 执行之前加入业务访问约束。
