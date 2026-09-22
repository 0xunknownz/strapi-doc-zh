# 📖 对照翻译：How to pass data from server to admin panel with a Strapi plugin

> Source: `docusaurus/docs/cms/plugins-development/guides/pass-data-from-server-to-admin.md`  
> Upstream SHA: `b5b43c750bac82390b085e478d4c0ae57f90c449`

**Original:** The admin panel and server are separate. To pass server data to admin code, expose an admin route and call it with the authenticated admin fetch client.

**中文译文:** Strapi 是 headless architecture，plugin 的 `/server` 与 `/admin` 是两个独立 runtime：
- Server 可以访问 `strapi`、database、services；
- Admin panel 是 browser React application，不能直接调用 server-side `strapi` object。

因此数据传递模式是：

`Server controller → Admin route → getFetchClient() → React component`

## Create an admin route

```js title="/my-plugin/server/routes/index.js"
module.exports = {
  'pass-data': {
    type: 'admin',

    routes: [
      {
        method:
          'GET',

        path:
          '/pass-data',

        handler:
          'myPluginContentType.index',

        config: {
          policies: [],
          auth: false,
        },
      },
    ],
  },
};
```

**中文译文:** `type: 'admin'` 将 route 放入 admin router namespace。示例使用 `auth: false` 只是演示数据通道；真实敏感数据 route 通常应使用 admin authentication / RBAC。

## Controller

```js
module.exports = {
  async index(ctx) {
    ctx.body =
      'You are in the my-plugin-content-type controller!';
  },
};
```

## Fetch from admin code

```js
import {
  getFetchClient,
} from '@strapi/strapi/admin';

const {
  get,
} =
  getFetchClient();

const foobarRequests = {
  getFoobar:
    async () => {
      const {
        data,
      } =
        await get(
          '/my-plugin/pass-data'
        );

      return data;
    },
};

export default
  foobarRequests;
```

**中文译文:** `getFetchClient()` 自动使用 admin authentication，不需要自行管理 token。

## Use from React

```js
useEffect(() => {
  foobarRequests
    .getFoobar()
    .then((data) => {
      setFoobar(data);
    });
}, [setFoobar]);
```

**中文译文:** 对更复杂 request，推荐进一步封装 API client / React data hook，并处理 loading、error、cancellation。
