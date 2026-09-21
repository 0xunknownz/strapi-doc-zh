# 📖 对照翻译：Users & Permissions GraphQL API

> Source: `docusaurus/docs/cms/features/users-permissions/graphql-api.md`  
> Upstream SHA: `2a6f846dd8a04268b50459499049e5cf36012bfc`

**Original:** The Users & Permissions feature provides GraphQL queries and mutations for authentication, user management, and role-based access.

**中文译文:** Users & Permissions feature 提供用于 authentication、user management 和 role-based access 的 GraphQL queries 与 mutations。

**Original:** This page documents all GraphQL queries and mutations provided by Users & Permissions. The GraphQL plugin must be installed.

**中文译文:** 本页记录 Users & Permissions 提供的全部 GraphQL queries 与 mutations。使用前必须安装 [GraphQL plugin](/cms/plugins/graphql)。功能配置请参阅 [Users & Permissions](/cms/features/users-permissions)。

## Authentication

**Original:** Authentication mutations handle login, registration, and password management. Public mutations do not require an Authorization header.

**中文译文:** Authentication mutations 用于 login、registration 和 password management。Public mutations 不需要 `Authorization` header。

### Login

**Original:** The `login` mutation authenticates a user and returns a JWT:

```graphql
mutation {
  login(input: { identifier: "user@example.com", password: "yourPassword" }) {
    jwt
    user {
      id
      documentId
      username
      email
      confirmed
      blocked
    }
  }
}
```

Input: `UsersPermissionsLoginInput` — `identifier` (String!), `password` (String!), `provider` (String, default "local"). Returns `UsersPermissionsLoginPayload`. Auth: Public.

**中文译文:** `login` mutation 对用户进行 authentication 并返回 JWT。输入类型为 `UsersPermissionsLoginInput`：`identifier`（email 或 username）、`password`、可选 `provider`（默认 `local`）。返回 `UsersPermissionsLoginPayload`。Auth：Public。GraphQL 代码保持原样。

### Register

**Original:** The `register` mutation creates a new user and returns a JWT:

```graphql
mutation {
  register(input: { username: "newuser", email: "new@example.com", password: "Password123!" }) {
    jwt
    user {
      id
      documentId
      username
      email
    }
  }
}
```

Input: username, email, password. Auth: Public.

**中文译文:** `register` mutation 创建新 user account 并返回 JWT。输入包括 `username`、`email`、`password`，均为必填。Auth：Public。默认只接受这 3 个字段；其他字段需要通过 `register.allowedFields` 配置。

### Forgot password

**Original:**

```graphql
mutation {
  forgotPassword(email: "user@example.com") {
    ok
  }
}
```

The mutation sends a password-reset email. Input is direct argument `email`. Returns `UsersPermissionsPasswordPayload`. Auth: Public.

**中文译文:** `forgotPassword` mutation 会发送 password reset email。输入是直接参数 `email`，不是 input object。返回 `UsersPermissionsPasswordPayload`，其中包含 `ok`。Auth：Public。

### Reset password

**Original:**

```graphql
mutation {
  resetPassword(code: "resetTokenFromEmail", password: "NewPassword123!", passwordConfirmation: "NewPassword123!") {
    jwt
    user {
      id
      username
      email
    }
  }
}
```

Inputs: `code`, `password`, `passwordConfirmation`. Returns login payload. Auth: Public.

**中文译文:** `resetPassword` 使用 email 中收到的 reset token 设置新 password。输入直接参数：`code`、`password`、`passwordConfirmation`。返回 login payload。Auth：Public。

### Change password

**Original:**

```graphql
mutation {
  changePassword(currentPassword: "OldPassword123!", password: "NewPassword456!", passwordConfirmation: "NewPassword456!") {
    jwt
    user {
      id
      username
      email
    }
  }
}
```

Requires Authorization Bearer token. Auth: Authenticated.

**中文译文:** `changePassword` 更新当前 authenticated user 的 password。请求必须包含 Bearer token 的 `Authorization` header。输入 `currentPassword`、`password`、`passwordConfirmation`。Auth：Authenticated。

### Email confirmation

**Original:**

```graphql
mutation {
  emailConfirmation(confirmation: "confirmationTokenFromEmail") {
    jwt
    user {
      id
      username
      email
      confirmed
    }
  }
}
```

The GraphQL mutation returns JWT and user directly, unlike the REST equivalent which redirects.

**中文译文:** `emailConfirmation` 使用 email 中收到的 confirmation token 确认用户 email address。与会执行 redirect 的 REST equivalent 不同，GraphQL mutation 会直接返回 JWT 和 user object。Auth：Public。

## User queries and mutations

**Original:** These operations manage user records and require corresponding permissions. User and role mutations accept numeric database `id`, not `documentId`.

**中文译文:** 这些 operations 用于查询和管理 user records，需要 requesting user's role 拥有对应 permission。User 与 role mutations 的 `id` 参数接受 numeric database `id`，**不接受** `documentId`；`documentId` 只用于 response reference。

### Get authenticated user

```graphql
query {
  me {
    id
    documentId
    username
    email
    confirmed
    blocked
    role {
      id
      name
      description
      type
    }
  }
}
```

**中文译文:** `me` query 返回当前 authenticated user 的 profile。需要 `Authorization` header，返回 `UsersPermissionsMe`。

### Create a user

```graphql
mutation {
  createUsersPermissionsUser(data: { username: "newuser", email: "new@example.com", password: "Password123!" }) {
    data {
      documentId
      username
      email
    }
  }
}
```

**Original:** Input is `UsersPermissionsUserInput`. Requires `plugin::users-permissions.user.create`.

**中文译文:** 输入为根据 User content-type schema 自动生成、并额外包含 `password` 的 `UsersPermissionsUserInput`。需要 `plugin::users-permissions.user.create` permission。

### Update a user

```graphql
mutation {
  updateUsersPermissionsUser(id: "1", data: { username: "updatedname" }) {
    data {
      documentId
      username
      email
    }
  }
}
```

**Original:** Requires `plugin::users-permissions.user.update`.

**中文译文:** `updateUsersPermissionsUser` 更新已有 user record，需要 `plugin::users-permissions.user.update` permission。

### Delete a user

```graphql
mutation {
  deleteUsersPermissionsUser(id: "1") {
    data {
      documentId
      username
    }
  }
}
```

**Original:** Requires `plugin::users-permissions.user.destroy`.

**中文译文:** `deleteUsersPermissionsUser` 删除 user record，需要 `plugin::users-permissions.user.destroy` permission。

## Role mutations

**Original:** Role mutations manage end-user roles and return `{ ok: true }` on success.

**中文译文:** Role mutations 用于管理 end-user roles，成功时返回 `{ ok: true }`，不会直接返回 role data。

### Create a role

```graphql
mutation {
  createUsersPermissionsRole(data: { name: "Editor", description: "Can edit content" }) {
    ok
  }
}
```

**中文译文:** 创建 role 需要 `plugin::users-permissions.role.createRole` permission。

### Update a role

```graphql
mutation {
  updateUsersPermissionsRole(id: "1", data: { name: "Senior Editor", description: "Can edit and publish" }) {
    ok
  }
}
```

**中文译文:** 更新 role 需要 `plugin::users-permissions.role.updateRole` permission。

### Delete a role

```graphql
mutation {
  deleteUsersPermissionsRole(id: "3") {
    ok
  }
}
```

**中文译文:** 删除 role 需要 `plugin::users-permissions.role.deleteRole` permission。Public role 不能删除。

## Session management

**Original:** Token refresh and logout are only available through REST API. There are no GraphQL equivalents.

**中文译文:** Token refresh 和 logout 只通过 [REST API](/cms/features/users-permissions/rest-api#session-management) 提供，没有 GraphQL equivalents。

## Types reference

**Original:**

| Type | Fields | Used by |
|---|---|---|
| `UsersPermissionsLoginInput` | `identifier`, `password`, `provider` | `login` |
| `UsersPermissionsRegisterInput` | `username`, `email`, `password` | `register` |
| `UsersPermissionsLoginPayload` | `jwt`, `user` | login/register/reset/change/confirmation |
| `UsersPermissionsPasswordPayload` | `ok` | forgotPassword |
| `UsersPermissionsMe` | id, documentId, username, email, confirmed, blocked, role | `me`, login payload |
| `UsersPermissionsMeRole` | id, name, description, type | nested role |

**中文译文:** 主要 GraphQL types：

| Type | Fields | 用途 |
|---|---|---|
| `UsersPermissionsLoginInput` | `identifier`、`password`、`provider` | `login` |
| `UsersPermissionsRegisterInput` | `username`、`email`、`password` | `register` |
| `UsersPermissionsLoginPayload` | `jwt`、`user` | login / register / resetPassword / changePassword / emailConfirmation |
| `UsersPermissionsPasswordPayload` | `ok` | forgotPassword |
| `UsersPermissionsMe` | id、documentId、username、email、confirmed、blocked、role | `me` 与 login payload |
| `UsersPermissionsMeRole` | id、name、description、type | `UsersPermissionsMe` 中的 role |
