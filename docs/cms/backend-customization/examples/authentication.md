# 📖 对照翻译：Examples cookbook — Authentication flow with JWT

> Source: `docusaurus/docs/cms/backend-customization/examples/authentication.md`  
> Upstream SHA: `c8651e5ff1bf15b9e4aa2b9c91c60da494b43883`

**Original:** Authenticate REST API requests using JWT by sending credentials to the `/auth/local` endpoint and storing the token in `localStorage`, with optional session management for refresh token support.

**中文译文:** 通过向 `/auth/local` endpoint 提交 credentials 获取 JWT，并将 token 保存到 `localStorage`，即可为后续 REST API request 提供 authentication。也可以启用 session management，以支持短期 access token 与 refresh token。

**Original:** This page is part of the backend customization examples cookbook.

**中文译文:** 本页面属于 Backend customization examples cookbook。建议先阅读 [cookbook introduction](/cms/backend-customization/examples)。

## Context and goal

**Original:** FoodAdvisor does not provide a front-end login flow out of the box. The goal is to add a basic login page to the Next.js application in `/client`.

**中文译文:** FoodAdvisor 默认没有 front-end login flow。本示例在 `/client` 中的 Next.js application 添加一个基础 login page，用于程序化 authentication Strapi Content API request。

**Original:** The component should:
1. display a login form,
2. send a request to `/auth/local`,
3. receive a JWT,
4. store it in browser `localStorage`.

**中文译文:** 目标流程：
1. 显示 email / password login form；
2. 向 Strapi back end 的 `/auth/local` 发送 request；
3. 从 response 中取得 JWT；
4. 把 JWT 保存到 browser `localStorage`，供后续 request 使用。

**Original:** Additional JWT authentication details are documented in Users & Permissions.

**中文译文:** JWT authentication 的完整机制请参阅 [Users & Permissions](/cms/features/users-permissions)。

## Basic JWT login example

**Original:** The example uses Formik. Install it with `yarn add formik` and restart the dev server.

**中文译文:** 示例使用 Formik。先运行 `yarn add formik` 安装 dependency，并重启 front-end development server。

**Original code (kept unchanged):**

```jsx title="/client/pages/auth/login.js"
import React from 'react';
import { useFormik } from 'formik';
import { Button, Input } from '@nextui-org/react';
import Layout from '@/components/layout';
import { getStrapiURL } from '@/utils';

const Login = () => {
  const { handleSubmit, handleChange } = useFormik({
    initialValues: {
      identifier: '',
      password: '',
    },
    onSubmit: async (values) => {
      const res = await fetch(getStrapiURL('/auth/local'), {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(values),
      });

      const { jwt } = await res.json();

      localStorage.setItem('token', jwt);
    },
  });

  return (
    <Layout>
      <div className="h-full w-full flex justify-center items-center my-24">
        <form onSubmit={handleSubmit} className="flex flex-col gap-y-6 w-4/12 ">
          <h1 className="font-bold text-3xl mb-6">Login</h1>
          <Input
            onChange={handleChange}
            type="email"
            name="identifier"
            label="Email"
            placeholder="Enter your email"
          />
          <Input
            type="password"
            name="password"
            label="Password"
            placeholder="Enter your password"
            onChange={handleChange}
          />
          <Button type="submit" className="bg-primary rounded-md text-muted">
            Login
          </Button>
        </form>
      </div>
    </Layout>
  );
};

export default Login;
```

**中文译文:** 关键逻辑保持原样：
- `getStrapiURL('/auth/local')` 根据项目 API prefix 生成正确的 authentication URL；
- request body 包含 `identifier` 与 `password`；
- Strapi 返回 `{ jwt, user }`；
- 示例只取 `jwt` 并写入 `localStorage.setItem('token', jwt)`。

该实现主要用于演示 authentication flow。真实 production 项目应根据前端安全架构选择更合适的 token storage / session strategy。

## Enhanced authentication with session management

**Original:** Session management provides shorter-lived access tokens and refresh token functionality.

**中文译文:** 启用 Users & Permissions session management 后，可以使用较短生命周期的 access token，并通过 refresh token 延长登录会话。

### Configuration

**Original code (kept unchanged):**

```js title="/config/plugins.js"
module.exports = ({ env }) => ({
  'users-permissions': {
    config: {
      jwtManagement: 'refresh',
      sessions: {
        accessTokenLifespan: 600,
        maxRefreshTokenLifespan: 2592000,
        idleRefreshTokenLifespan: 1209600,
        maxSessionLifespan: 86400,
        idleSessionLifespan: 7200,
      },
    },
  },
});
```

**中文译文:** 上面的配置启用 `jwtManagement: 'refresh'`，并配置 access token、refresh token 与 session 的生命周期。代码保持原样。

### Enhanced login behavior

**Original:** In session-management mode, the login response can contain both `jwt` and `refreshToken`. Store both; in legacy mode only store `jwt`.

**中文译文:** 启用 refresh 模式后，login response 可以同时包含：
- `jwt`：access token；
- `refreshToken`：用于刷新 access token。

示例会根据 response 自动兼容两种模式：
- 有 `refreshToken`：保存 `accessToken` 与 `refreshToken`；
- 没有 `refreshToken`：按 legacy 模式保存 `token`。

**Original code (core section kept unchanged):**

```js
const data = await res.json();

if (res.ok) {
  if (data.refreshToken) {
    localStorage.setItem('accessToken', data.jwt);
    localStorage.setItem('refreshToken', data.refreshToken);
  } else {
    localStorage.setItem('token', data.jwt);
  }

  window.location.href = '/dashboard';
} else {
  console.error('Login failed:', data.error);
}
```

**中文译文:** 成功后示例跳转到 `/dashboard`；失败时记录 Strapi 返回的 error。真实项目还应实现 refresh endpoint 调用、token expiration 处理与 logout/session revocation。

**Original:** Next, learn how services and controllers can further customize a Strapi application.

**中文译文:** 下一步可继续阅读 [Custom services and controllers](/cms/backend-customization/examples/services-and-controllers)。
