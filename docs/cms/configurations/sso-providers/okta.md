# 📖 对照翻译：Okta provider SSO configuration

> Source: `docusaurus/docs/cms/configurations/sso-providers/okta.md`  
> Upstream SHA: `474a3570d2fbede4018a2a20b8f06c408f085778`

**Original:** Okta allows users to sign in and sign up to Strapi using OAuth2 credentials configured in the `auth.providers` array.

**中文译文:** Okta 可以作为 Strapi admin SSO provider。通过在 `config/admin` 的 `auth.providers` 中配置 OAuth2 credentials，administrator 可以使用 Okta account 登录。

## Installation

```bash
# yarn
yarn add passport-okta-oauth20

# npm
npm install --save passport-okta-oauth20
```

## Important domain requirement

**Original:** `OKTA_DOMAIN` must include the protocol, e.g. `https://example.okta.com`, otherwise you can get a redirect loop.

**中文译文:** **`OKTA_DOMAIN` 必须包含 protocol**，例如：
`https://example.okta.com`

如果只写 `example.okta.com`，OAuth flow 可能陷入 redirect loop。

## Configuration

**Original code (kept unchanged):**

```js title="/config/admin.js"
const OktaOAuth2Strategy = require("passport-okta-oauth20").Strategy;

module.exports = ({ env }) => ({
  auth: {
    providers: [
      {
        uid: "okta",
        displayName: "Okta",
        icon: "https://www.okta.com/sites/default/files/Okta_Logo_BrightBlue_Medium-thumbnail.png",
        createStrategy: (strapi) =>
          new OktaOAuth2Strategy(
            {
              clientID: env("OKTA_CLIENT_ID"),
              clientSecret: env("OKTA_CLIENT_SECRET"),
              audience: env("OKTA_DOMAIN"),
              scope: ["openid", "email", "profile"],
              callbackURL:
                strapi.admin.services.passport.getStrategyCallbackURL("okta"),
            },
            (accessToken, refreshToken, profile, done) => {
              done(null, {
                email: profile.email,
                username: profile.username,
              });
            }
          ),
      },
    ],
  },
});
```

**中文译文:** 配置项：
- `OKTA_CLIENT_ID`
- `OKTA_CLIENT_SECRET`
- `OKTA_DOMAIN`
- Scopes：`openid`、`email`、`profile`

Strategy callback 将 Okta profile 的 `email` 与 `username` 映射到 Strapi admin identity。

TypeScript 版本使用 `Strategy as OktaOAuth2Strategy`。
