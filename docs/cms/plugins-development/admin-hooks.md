# 📖 对照翻译：Admin Panel API — Hooks

> Source: `docusaurus/docs/cms/plugins-development/admin-hooks.md`  
> Upstream SHA: `a45ef8d308d2613e2eb65ab32d001188617a8e6e`

**Original:** The Hooks API lets plugins create extension points with `createHook` and subscribe to them with `registerHook`.

**中文译文:** Hooks API 允许 plugin 在 admin panel 中创建可扩展点，并让其他 plugin 订阅这些事件：
- `createHook()`：在 `register()` lifecycle 声明 hook；
- `registerHook()`：在 `bootstrap()` lifecycle 订阅 hook。

## Creating hooks

```js
export default {
  register(app) {
    app.createHook(
      'my-plugin/my-hook'
    );
  },
};
```

**中文译文:** 建议使用稳定、带 plugin namespace 的 hook ID，例如 `my-plugin/my-hook`，避免不同 plugin 之间冲突。

## Subscribing

```js
export default {
  bootstrap(app) {
    app.registerHook(
      'my-plugin/my-hook',
      (...args) => {
        console.log(args);
        return args;
      }
    );
  },
};
```

**Original:** Async callbacks are supported.

**中文译文:** Subscriber 可以是 async function。对于 waterfall hook，必须把处理后的值 return 给下一个 subscriber。

## Running hooks

| Mode | Function | 中文说明 |
|---|---|---|
| Series | `runHookSeries` | 顺序执行，返回每个 callback 的结果 array |
| Parallel | `runHookParallel` | 并行执行 async callbacks，返回 resolved results |
| Waterfall | `runHookWaterfall` | 前一个 callback 的返回值传给下一个，最终返回单个结果 |

**Original:** A waterfall subscriber that does not return a value breaks the chain.

**中文译文:** **Waterfall hook 中每个 subscriber 必须 return transformed value。** 返回 `undefined` 会导致后续 subscriber 无法收到正确数据。

## Predefined Content Manager hooks

### `INJECT-COLUMN-IN-TABLE`

**Original:** `Admin/CM/pages/ListView/inject-column-in-table` can add or mutate List View columns.

**中文译文:** Content Manager List View 提供：

`Admin/CM/pages/ListView/inject-column-in-table`

可用于增加 / 修改列表 columns。

```js
export default {
  bootstrap(app) {
    app.registerHook(
      'Admin/CM/pages/ListView/inject-column-in-table',
      ({ displayedHeaders, layout }) => ({
        displayedHeaders: [
          ...displayedHeaders,
          {
            attribute: {
              type: 'custom',
            },
            label: 'External id',
            name: 'externalId',
            searchable: false,
            sortable: false,
            cellFormatter:
              (document) =>
                document.externalId,
          },
        ],
        layout,
      })
    );
  },
};
```

**中文译文:** 示例向 List View 增加一个 custom `External id` column，并通过 `cellFormatter` 从 document 读取展示值。

### `MUTATE-EDIT-VIEW-LAYOUT`

**Original:** `Admin/CM/pages/EditView/mutate-edit-view-layout` can mutate the Content Manager Edit View layout.

**中文译文:** Edit View 提供：

`Admin/CM/pages/EditView/mutate-edit-view-layout`

用于调整 edit form layout。

```js
export default {
  bootstrap(app) {
    app.registerHook(
      'Admin/CM/pages/EditView/mutate-edit-view-layout',
      ({ layout, ...rest }) => {
        const updatedLayout =
          layout.map((rowGroup) =>
            rowGroup.map((row) =>
              row.map((field) => ({
                ...field,
                size: 12,
              }))
            )
          );

        return {
          ...rest,
          layout: updatedLayout,
        };
      }
    );
  },
};
```

**中文译文:** 上例把默认 Edit View 中全部 fields 强制设为 12-column full width。

**Original:** Plugin authors should use the documented `EditLayout` and `ListLayout` shapes rather than relying on internal package paths.

**中文译文:** Internal package naming 可能随版本改变。Plugin 应依赖文档公开的 `EditLayout` / `ListLayout` 数据 shape，而不是直接耦合内部 source path。
