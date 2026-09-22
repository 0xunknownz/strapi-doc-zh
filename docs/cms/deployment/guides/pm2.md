# 📖 对照翻译：Running Strapi with PM2

> Source: `docusaurus/docs/cms/deployment/guides/pm2.md`  
> Upstream SHA: `617e804157e47be3d700a1d9766185b5ab95a43f`

**Original:** Build the admin panel, define the application in `ecosystem.config.js` with `NODE_ENV=production`, then use PM2 to keep it running and restore it after reboot.

**中文译文:** PM2 用于让 Strapi process 在 shell 退出或 crash 后继续运行，并提供 restart、logs 与 reboot recovery。Production 流程是先 build admin panel，再通过 `ecosystem.config.js` 启动。

## Install PM2

```bash
# Yarn
yarn global add pm2

# NPM
npm install -g pm2
```

## Build the admin panel

```bash
# Yarn
NODE_ENV=production yarn build

# NPM
NODE_ENV=production npm run build
```

**Original:** Do not export `NODE_ENV=production` before dependency installation, or devDependencies required by the build can be skipped.

**中文译文:** 不要在安装 dependencies 之前把整个 shell session 都设成 `NODE_ENV=production`，否则 package manager 可能跳过 build 所需 devDependencies。最好只在 build command 上设置。

## Ecosystem file

```js title="/ecosystem.config.js"
module.exports = {
  apps: [
    {
      name: 'strapi',
      cwd: '/srv/strapi',
      script: 'npm',
      args: 'start',
      env: {
        NODE_ENV: 'production',
        HOST: '0.0.0.0',
        PORT: 1337,
      },
    },
  ],
};
```

**中文译文:** 
- `name`：PM2 process name；
- `cwd`：项目 absolute path；
- `script + args`：保持与手动 `npm start` 一致；
- `env`：process environment。

Secrets 不要提交到 ecosystem file，应放在 server `.env` 或 deployment secret manager。

## Start and inspect

```bash
pm2 start ecosystem.config.js
pm2 list
pm2 logs strapi --lines 100
```

## Survive reboot

```bash
pm2 startup
# 执行 PM2 输出的 sudo command
pm2 save
```

**中文译文:** 每次新增 / 删除 / 重命名 application 后，都应再次 `pm2 save`。

## Log rotation

```bash
pm2 install pm2-logrotate
pm2 set pm2-logrotate:max_size 10M
pm2 set pm2-logrotate:retain 7
```

## Deploy an update

**Original:** Fetch code, install dependencies, build, then restart with updated environment.

```bash
pm2 restart strapi --update-env
```

**中文译文:** 推荐顺序：
1. Pull/fetch 新代码；
2. 安装 dependencies；
3. `NODE_ENV=production` build admin；
4. `pm2 restart strapi --update-env`。

不加 `--update-env` 时，PM2 可能继续复用旧 environment。

## Cluster mode

**Original:** PM2 cluster mode requires a JavaScript entry point rather than `script: 'npm'`.

```js title="/server.js"
const strapi = require('@strapi/strapi');

strapi.createStrapi().start();
```

**中文译文:** TypeScript project 需给 `createStrapi` 传 `distDir`。Cluster mode 下配置：

```js
script: './server.js',
exec_mode: 'cluster',
instances: 'max',
```

**中文译文:** 开启前务必阅读 multi-instance caveats：schema migration、cron、in-memory state、local upload 都需要额外设计。

## Verify

```bash
pm2 list
curl -I http://localhost:1337/_health
```

**中文译文:** 再实际 reboot server，并确认 PM2 自动恢复 Strapi。

## Troubleshooting

**中文译文:**
- `errored`：查看 `pm2 logs`，常见原因是缺 build、DB unreachable、环境变量缺失；
- Restart loop：先 `pm2 stop strapi` 再排错；
- Reboot 后未恢复：重新执行 `pm2 startup` 与 `pm2 save`；
- 新 env 不生效：使用 `--update-env`；
- Admin 仍是旧版本：重新 build 后 restart。
