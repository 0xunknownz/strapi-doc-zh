# 📖 对照翻译：Google provider SSO configuration

> Source: `docusaurus/docs/cms/configurations/sso-providers/google.md`  
> Upstream SHA: `20654950ab63365cf57d70c09d5be8537626bece`

**Original:** Configure Google as an SSO provider in your Strapi admin panel to allow users to sign in and sign up using their Google account credentials.

**中文译文:** 可以将 Google 配置为 Strapi admin SSO provider，让 administrator 使用 Google account 完成 sign-in / sign-up。

## Installation

```bash
# yarn
yarn add passport-google-oauth2

# npm
npm install --save passport-google-oauth2
```

## Configuration

**Original code (kept unchanged):**

```js title="/config/admin.js"
const GoogleStrategy = require("passport-google-oauth2");

module.exports = ({ env }) => ({
  auth: {
    providers: [
      {
        uid: "google",
        displayName: "Google",
        icon: "https://cdn2.iconfinder.com/data/icons/social-icons-33/128/Google-512.png",
        createStrategy: (strapi) =>
          new GoogleStrategy(
            {
              clientID: env("GOOGLE_CLIENT_ID"),
              clientSecret: env("GOOGLE_CLIENT_SECRET"),
              scope: [
                "https://www.googleapis.com/auth/userinfo.email",
                "https://www.googleapis.com/auth/userinfo.profile",
              ],
              callbackURL:
                strapi.admin.services.passport.getStrategyCallbackURL("google"),
            },
            (request, accessToken, refreshToken, profile, done) => {
              done(null, {
                email: profile.email,
                firstname: profile.given_name,
                lastname: profile.family_name,
              });
            }
          ),
      },
    ],
  },
});
```

**中文译文:** 关键点：
- `GOOGLE_CLIENT_ID` / `GOOGLE_CLIENT_SECRET` 来自 Google OAuth application；
- Scope 同时请求 user email 与 profile；
- callback 映射 `profile.email`、`given_name`、`family_name`；
- callback URL 通过 Strapi Passport service 动态生成。

TypeScript 版本使用 `Strategy as GoogleStrategy`，配置语义相同。
