# 📖 对照翻译：Discord provider SSO configuration

> Source: `docusaurus/docs/cms/configurations/sso-providers/discord.md`  
> Upstream SHA: `1e9357bd8054cadf79ec5c49cafb7e662ca6b44b`

**Original:** Discord SSO provider enables users to sign in and sign up to Strapi through their Discord account. Configure it in `config/admin` using `passport-discord` with client credentials and email scope.

**中文译文:** Discord SSO provider 允许 administrator 使用 Discord account 登录或注册 Strapi admin panel。配置位于 `config/admin.js|ts` 的 `auth.providers`，并使用 `passport-discord` strategy、Discord client credentials 与 email scope。

**Original:** Prerequisite: read the general SSO configuration guide.

**中文译文:** 前置条件：先阅读 [How to configure SSO](/cms/configurations/guides/configure-sso)，了解 callback URL、admin SSO settings 与 provider 注册结构。

## Installation

```bash
# yarn
yarn add passport-discord

# npm
npm install --save passport-discord
```

**中文译文:** 安装 `passport-discord`。命令保持原样。

## Configuration

**Original code (kept unchanged):**

```js title="/config/admin.js"
const DiscordStrategy = require("passport-discord");

module.exports = ({ env }) => ({
  auth: {
    providers: [
      {
        uid: "discord",
        displayName: "Discord",
        icon: "https://cdn0.iconfinder.com/data/icons/free-social-media-set/24/discord-512.png",
        createStrategy: (strapi) =>
          new DiscordStrategy(
            {
              clientID: env("DISCORD_CLIENT_ID"),
              clientSecret: env("DISCORD_SECRET"),
              callbackURL:
                strapi.admin.services.passport.getStrategyCallbackURL(
                  "discord"
                ),
              scope: ["identify", "email"],
            },
            (accessToken, refreshToken, profile, done) => {
              done(null, {
                email: profile.email,
                username: `${profile.username}#${profile.discriminator}`,
              });
            }
          ),
      },
    ],
  },
});
```

**中文译文:** 关键点：
- `DISCORD_CLIENT_ID`：Discord OAuth application client ID；
- `DISCORD_SECRET`：client secret；
- `scope: ["identify", "email"]`：需要 identity 与 email；
- callback 使用 `getStrategyCallbackURL("discord")`，避免硬编码；
- Strategy callback 将 Discord profile 映射为 Strapi admin user 的 `email` 与 `username`。

TypeScript 版本使用 `import { Strategy as DiscordStrategy } from "passport-discord"`，其余配置相同。
