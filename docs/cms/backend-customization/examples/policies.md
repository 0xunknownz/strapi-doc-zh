# 📖 对照翻译：Examples cookbook — Custom policies

> Source: `docusaurus/docs/cms/backend-customization/examples/policies.md`  
> Upstream SHA: `5bdad1d67debe2a2988bb8489e162277e3fe5429`

**Original:** Custom policies control access to content-type endpoints by allowing or blocking requests, and can throw custom errors using `PolicyError` for better error handling and front-end integration.

**中文译文:** Custom policy 可以在 request 到达 controller 前允许或阻止访问。除了简单返回 `true` / `false`，还可以抛出 `PolicyError`，向 front end 返回更明确的 error message 与 machine-readable error code。

**Original:** Policies are read-only checks; route middlewares can perform additional logic.

**中文译文:** Policy 主要承担 read-only authorization / validation；如果需要修改 request context 或执行更多流程控制，通常应使用 route middleware。

## Creating a custom policy

**Original:** Goal: prevent restaurant owners from submitting fake reviews for their own businesses.

**中文译文:** 示例目标：FoodAdvisor 中禁止 restaurant owner 为自己经营的 restaurant 提交 review。

**Original:** Steps:
1. Add a policy under the Reviews API.
2. Read request body and authenticated user.
3. Query the restaurant with Document Service API and populate its owner.
4. Block if requester is the owner.

**中文译文:** 核心流程：
1. 在 Reviews API 下创建 policy；
2. 从 `policyContext.request` 与 `policyContext.state` 读取 request body 和 authenticated user；
3. 使用 Document Service API 查询 restaurant，并 populate owner；
4. 如果当前 user id 与 restaurant owner id 相同，则拒绝；否则允许。

**Original code (kept unchanged):**

```js title="src/api/review/policies/is-owner-review.js"
module.exports = async (policyContext, config, { strapi }) => {
  const { body } = policyContext.request;
  const { user } = policyContext.state;

  if (!user) {
    return false;
  }

  const [restaurant] = await strapi.documents('api::restaurant.restaurant').findMany({
    filters: {
      slug: body.restaurant,
    },
    populate: ['owner'],
  });

  if (!restaurant) {
    return false;
  }

  if (user.id === restaurant.owner.id) {
    return false;
  }

  return true;
};
```

**中文译文:** 该 policy：
- 没有 authenticated user 时直接拒绝；
- 根据 review body 中的 restaurant slug 查询目标 restaurant；
- population `owner`；
- requester 与 owner 相同则拒绝；
- 其他情况返回 `true`。

**Original:** A policy or route middleware must be declared in a route configuration to take effect.

**中文译文:** Policy 文件存在并不会自动生效。必须在对应 route 的 configuration 中声明，详见 [Routes](/cms/backend-customization/routes) 或本 cookbook 的 [Custom routes](/cms/backend-customization/examples/routes)。

## Sending custom errors through policies

**Original:** Instead of returning `false`, a policy can throw `PolicyError` with a custom message and details.

**中文译文:** 如果简单返回 `false`，Strapi 会返回 generic `Policy Failed`。为了给 front end 更明确的信息，可以抛出 `PolicyError`。

**Original code (core section kept unchanged):**

```js
const { errors } = require('@strapi/utils');
const { PolicyError } = errors;

if (user.id === restaurant.owner.id) {
  throw new PolicyError(
    'The owner of the restaurant cannot submit reviews',
    {
      errCode: 'RESTAURANT_OWNER_REVIEW',
    }
  );
}
```

**中文译文:** 这里自定义了：
- Human-readable message：`The owner of the restaurant cannot submit reviews`；
- Machine-readable detail：`errCode: 'RESTAURANT_OWNER_REVIEW'`。

### Default error response

```json
{
  "data": null,
  "error": {
    "status": 403,
    "name": "PolicyError",
    "message": "Policy Failed",
    "details": {}
  }
}
```

### Custom error response

```json
{
  "data": null,
  "error": {
    "status": 403,
    "name": "PolicyError",
    "message": "The owner of the restaurant cannot submit reviews",
    "details": {
      "policy": "is-owner-review",
      "errCode": "RESTAURANT_OWNER_REVIEW"
    }
  }
}
```

**中文译文:** Custom error 让 front end 可以同时：
- 向用户显示明确说明；
- 根据 `errCode` 做稳定的程序化分支处理。

## Using custom errors on the front end

**Original:** The FoodAdvisor front end can catch the API error and display a toast, while showing a success toast when the review is created.

**中文译文:** Front end 可以解析 Strapi response 中的 `error`，将 `error.message` 显示为 toast；成功创建 review 时则显示 success notification。

**Original code (core handling kept unchanged):**

```js
const { data, error } = await res.json();

if (error) {
  throw new UnauthorizedError(error.message);
}

toast.success('Review created!');
return data;
```

**中文译文:** 这样 policy 从“后端访问控制”延伸为完整 UX：后端提供清晰 error contract，前端根据 contract 显示用户可理解的反馈。

**Original:** Next, configure custom routes to use custom policies.

**中文译文:** 下一步参阅 [Custom routes](/cms/backend-customization/examples/routes)，将 policy 绑定到实际 endpoint。
