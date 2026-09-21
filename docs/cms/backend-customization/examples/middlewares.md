# 📖 对照翻译：Examples cookbook — Custom global middlewares

> Source: `docusaurus/docs/cms/backend-customization/examples/middlewares.md`  
> Upstream SHA: `81f9512f630f421f9f560eda30ffc9e5ca6bd44e`

**Original:** Custom global middlewares intercept incoming requests before controller execution, enabling logic such as analytics tracking. This example logs restaurant page visits to Google Sheets.

**中文译文:** Custom global middleware 可以在 controller 执行之前拦截 request，适合 analytics、logging、header processing 等横切逻辑。本示例在访问 restaurant page 时，将浏览次数写入 Google Sheets。

**Original:** Strapi has route middlewares and global middlewares. Route middlewares have a narrower scope; global middlewares have a wider scope.

**中文译文:** Strapi 中 route middleware 与 global middleware 的 scope 不同：
- route middleware：绑定单个或少量 routes；
- global middleware：作用范围更广，可以覆盖 application / API 请求链。

**Original:** This example focuses on custom global middleware rather than route middleware.

**中文译文:** 本页重点演示 global-style analytics middleware，而不是使用 route middleware 做 authorization。

## Goal

**Original:**
- Build Google Sheets utility functions.
- Run middleware for incoming restaurant-page requests.
- Create/update a Google Sheet with page-view data.
- Attach middleware to the desired route.

**中文译文:** 目标：
- 创建 Google Sheets read/write/update utility；
- 每次 Restaurant detail request 到达时执行 analytics middleware；
- 根据 restaurant 是否已存在于 spreadsheet 中，新增记录或累加 views；
- 把 middleware 绑定到 `findOne` route。

## Google Sheets utility

**Original:** The utility creates an authenticated Google Sheets client and exposes `writeGoogleSheet`, `updateoogleSheet`, and `readGoogleSheet`.

**中文译文:** `utils.js` 使用 service account key 创建 Google Sheets API client，并封装：
- `writeGoogleSheet()`：append rows；
- `updateoogleSheet()`：更新指定 cell；
- `readGoogleSheet()`：读取当前 spreadsheet data。

**Original code (abbreviated only in prose; identifiers unchanged):**

```js
const { google } = require('googleapis');

const createGoogleSheetClient = async ({
  keyFile,
  sheetId,
  tabName,
  range,
}) => {
  const auth = new google.auth.GoogleAuth({
    keyFile,
    scopes: ['https://www.googleapis.com/auth/spreadsheets'],
  });

  const authClient = await auth.getClient();
  const googleSheetClient = google.sheets({
    version: 'v4',
    auth: authClient,
  });

  // ... writeGoogleSheet / updateoogleSheet / readGoogleSheet ...

  return {
    writeGoogleSheet,
    updateoogleSheet,
    readGoogleSheet,
  };
};
```

**中文译文:** 真实项目中应把 service account key 与 spreadsheet ID 放入安全配置 / environment variables，而不是硬编码到 source code。

## Analytics middleware

**Original:** The middleware reads the restaurant `documentId` from route params, loads the restaurant through Document Service, reads the sheet, then increments an existing view count or inserts a new row.

**中文译文:** Analytics middleware 的核心流程：
1. 从 `context.params.id` 获取 restaurant `documentId`；
2. 使用 `strapi.documents('api::restaurant.restaurant').findOne()` 查询 restaurant；
3. 读取 Google Sheet；
4. 如果已存在对应 restaurant，views + 1；
5. 如果不存在，新增一行并将 views 初始化为 1；
6. 最后 `await next()`，继续进入 controller。

**Original code (core middleware kept unchanged):**

```js
module.exports = (config, { strapi }) => {
  return async (context, next) => {
    const { readGoogleSheet, updateoogleSheet, writeGoogleSheet } =
      await createGoogleSheetClient({
        keyFile: serviceAccountKeyFile,
        range,
        sheetId,
        tabName,
      });

    const restaurantId = context.params.id;
    const restaurant = await strapi.documents('api::restaurant.restaurant').findOne({
      documentId: restaurantId,
    });

    const restaurantAnalytics = await readGoogleSheet();

    const requestedRestaurant =
      transformGSheetToObject(restaurantAnalytics)[restaurantId];

    if (requestedRestaurant) {
      await updateoogleSheet(
        `${VIEWS_CELL}${requestedRestaurant.cellNum}:${VIEWS_CELL}${requestedRestaurant.cellNum}`,
        [[Number(requestedRestaurant.views) + 1]]
      );
    } else {
      const newRestaurant = [[restaurant.id, restaurant.name, 1]];
      await writeGoogleSheet(newRestaurant);
    }

    await next();
  };
};
```

**中文译文:** `await next()` 很关键：analytics 处理完成后，request 才会继续进入后续 route/controller；如果提前 return，则会截断正常 request flow。

## Attach middleware to route

**Original code (kept unchanged):**

```js title="src/api/restaurant/routes/restaurant.js"
'use strict';

const { createCoreRouter } = require('@strapi/strapi').factories;

module.exports = createCoreRouter('api::restaurant.restaurant', {
  config: {
    findOne: {
      auth: false,
      policies: [],
      middlewares: ['api::restaurant.analytics'],
    },
  },
});
```

**中文译文:** 上例只在 restaurant `findOne` route 执行 analytics middleware。Middleware UID 使用 API-level naming：`api::restaurant.analytics`。
