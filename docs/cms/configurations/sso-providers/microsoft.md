# 📖 对照翻译：Microsoft provider SSO configuration

> Source: `docusaurus/docs/cms/configurations/sso-providers/microsoft.md`  
> Upstream SHA: `b0ae94d75ccc7d44a335f94bbeaa8ed3149b134b`

**Original:** Configure Microsoft SSO using `passport-azure-ad-oauth2`, allowing users to access Strapi admin through Microsoft accounts.

**中文译文:** Microsoft SSO 使用 `passport-azure-ad-oauth2` strategy，让 administrator 通过 Microsoft / Azure AD account 登录 Strapi admin panel。

## Installation

```bash
# yarn
yarn add passport-azure-ad-oauth2 jsonwebtoken

# npm
npm install --save passport-azure-ad-oauth2 jsonwebtoken
```

**中文译文:** 除 OAuth2 Passport strategy 外，还需要 `jsonwebtoken` 解码 Microsoft 返回的 `id_token`。

## Configuration

**Original code (kept unchanged):**

```js title="/config/admin.js"
const AzureAdOAuth2Strategy = require("passport-azure-ad-oauth2");
const jwt = require("jsonwebtoken");

module.exports = ({ env }) => ({
  auth: {
    providers: [
      {
        uid: "azure_ad_oauth2",
        displayName: "Microsoft",
        icon: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/96/Microsoft_logo_%282012%29.svg/320px-Microsoft_logo_%282012%29.svg.png",
        createStrategy: (strapi) =>
          new AzureAdOAuth2Strategy(
            {
              clientID: env("MICROSOFT_CLIENT_ID", ""),
              clientSecret: env("MICROSOFT_CLIENT_SECRET", ""),
              scope: ["user:email"],
              tenant: env("MICROSOFT_TENANT_ID", ""),
              callbackURL:
                strapi.admin.services.passport.getStrategyCallbackURL(
                  "azure_ad_oauth2"
                ),
            },
            (accessToken, refreshToken, params, profile, done) => {
              let waadProfile = jwt.decode(params.id_token, "", true);
              done(null, {
                email: waadProfile.email,
                username: waadProfile.email,
                firstname: waadProfile.given_name,
                lastname: waadProfile.family_name,
              });
            }
          ),
      },
    ],
  },
});
```

**中文译文:** 关键 environment variables：
- `MICROSOFT_CLIENT_ID`
- `MICROSOFT_CLIENT_SECRET`
- `MICROSOFT_TENANT_ID`

Strategy callback 使用 `jwt.decode(params.id_token, "", true)` 读取 Microsoft identity claims，再映射 `email`、`username`、`firstname`、`lastname`。

TypeScript 版本使用 `Strategy as AzureAdOAuth2Strategy` 和 `import jwt from "jsonwebtoken"`。
