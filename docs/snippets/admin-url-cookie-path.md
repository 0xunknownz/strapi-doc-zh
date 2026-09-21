# 📖 对照翻译：Admin URL and authentication cookie path

> Source: `docusaurus/docs/snippets/admin-url-cookie-path.md`  
> Upstream SHA: `23ab529eff987a26dd1243ed6980c3fa3a7abdce`

**Original:** Since Strapi 5.51, the admin authentication cookie path defaults to `/admin` regardless of `url`. When changing `url`, also set `auth.cookie.path` to the same value.

**中文译文:** 从 Strapi 5.51 开始，admin authentication cookie 的默认 path 固定为 `/admin`，不会自动跟随 `admin.url`。因此只要修改 admin `url`，就必须同步设置 `auth.cookie.path`。

**Original:** Otherwise login succeeds, but following requests are rejected and the panel returns to login.

**中文译文:** 如果两者不一致：
1. Login request 可能成功；
2. Browser 之后访问新 admin path 时无法读取旧 `/admin` scope 的 authentication cookie；
3. 后续 request 被拒绝；
4. Admin panel 无明显错误地重新跳回 login page。

**Original code (kept unchanged):**

```js title="/config/admin.js"
module.exports = ({ env }) => ({
  url: "/dashboard",
  auth: {
    cookie: {
      path: "/dashboard", // must match url
    },
  },
});
```

**中文译文:** `auth.cookie.path` 必须与 admin `url` 一致。

**Original:** Rebuild the admin after changing cookie path because the value is inlined into the admin bundle.

**中文译文:** 修改 `auth.cookie.path` 后必须重新 build admin panel，因为该值会在 build time inline 到 admin bundle。
