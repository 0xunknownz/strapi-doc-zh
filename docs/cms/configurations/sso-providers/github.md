# 📖 对照翻译：GitHub provider SSO configuration

> Source: `docusaurus/docs/cms/configurations/sso-providers/github.md`  
> Upstream SHA: `9027fa7b93caf68726e7436fbb23ae38873a6645`

**Original:** Configure GitHub as an SSO provider for Strapi admin sign-in using `passport-github2` in the `config/admin` file with your GitHub OAuth credentials and user email scope.

**中文译文:** 使用 `passport-github2` 可以把 GitHub 配置为 Strapi admin SSO provider。需要在 `config/admin.js|ts` 中提供 GitHub OAuth client credentials，并请求 `user:email` scope。

## Installation

```bash
# yarn
yarn add passport-github2

# npm
npm install --save passport-github2
```

## Configuration

**Original code (kept unchanged):**

```js title="/config/admin.js"
const GithubStrategy = require("passport-github2");

module.exports = ({ env }) => ({
  auth: {
    providers: [
      {
        uid: "github",
        displayName: "Github",
        icon: "https://cdn1.iconfinder.com/data/icons/logotypes/32/github-512.png",
        createStrategy: (strapi) =>
          new GithubStrategy(
            {
              clientID: env("GITHUB_CLIENT_ID"),
              clientSecret: env("GITHUB_CLIENT_SECRET"),
              scope: ["user:email"],
              callbackURL:
                strapi.admin.services.passport.getStrategyCallbackURL("github"),
            },
            (accessToken, refreshToken, profile, done) => {
              done(null, {
                email: profile.emails[0].value,
                username: profile.username,
              });
            }
          ),
      },
    ],
  },
});
```

**中文译文:** 关键 environment variables：
- `GITHUB_CLIENT_ID`
- `GITHUB_CLIENT_SECRET`

`user:email` scope 用于读取 GitHub account email。Strategy callback 将 `profile.emails[0].value` 与 `profile.username` 映射为 Strapi administrator identity。

TypeScript 版本使用 `import { Strategy as GithubStrategy } from "passport-github2"`。
