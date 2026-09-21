# 📖 对照翻译：Keycloak (OpenID Connect) provider SSO configuration

> Source: `docusaurus/docs/cms/configurations/sso-providers/keycloak.md`  
> Upstream SHA: `ee2a1cc6278a8a119492819b4e18cb20c5902e8b`

**Original:** Keycloak is an OpenID Connect SSO provider that lets users sign in to Strapi through Keycloak authentication using the `passport-keycloak-oauth2-oidc` strategy configured in `config/admin`.

**中文译文:** Keycloak 可作为 OpenID Connect SSO provider，通过 `passport-keycloak-oauth2-oidc` strategy 接入 Strapi admin authentication。

## Installation

```bash
# yarn
yarn add passport-keycloak-oauth2-oidc

# npm
npm install --save passport-keycloak-oauth2-oidc
```

## Configuration

**Original code (kept unchanged):**

```js title="/config/admin.js"
const KeyCloakStrategy = require("passport-keycloak-oauth2-oidc");

module.exports = ({ env }) => ({
  auth: {
    providers: [
      {
        uid: "keycloak",
        displayName: "Keycloak",
        icon: "https://raw.githubusercontent.com/keycloak/keycloak-admin-ui/main/themes/keycloak/logo.svg",
        createStrategy: (strapi) =>
          new KeyCloakStrategy(
            {
              clientID: env("KEYCLOAK_CLIENT_ID", ""),
              realm: env("KEYCLOAK_REALM", ""),
              publicClient: env.bool("KEYCLOAK_PUBLIC_CLIENT", false),
              clientSecret: env("KEYCLOAK_CLIENT_SECRET", ""),
              sslRequired: env("KEYCLOAK_SSL_REQUIRED", "external"),
              authServerURL: env("KEYCLOAK_AUTH_SERVER_URL", ""),
              callbackURL:
                strapi.admin.services.passport.getStrategyCallbackURL(
                  "keycloak"
                ),
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

**中文译文:** Keycloak 配置相比普通 OAuth provider 多出 realm / server settings：
- `KEYCLOAK_CLIENT_ID`
- `KEYCLOAK_REALM`
- `KEYCLOAK_PUBLIC_CLIENT`（Boolean）
- `KEYCLOAK_CLIENT_SECRET`
- `KEYCLOAK_SSL_REQUIRED`（默认 `external`）
- `KEYCLOAK_AUTH_SERVER_URL`

成功后从 Keycloak profile 映射 `email` 与 `username`。

TypeScript 版本使用 `Strategy as KeyCloakStrategy`。
