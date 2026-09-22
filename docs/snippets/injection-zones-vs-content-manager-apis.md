# 📖 对照翻译：Injection zones vs Content Manager APIs

> Source: `docusaurus/docs/snippets/injection-zones-vs-content-manager-apis.md`  
> Upstream SHA: `4de4f1fb4f218a28b2004fa291bbc39b36e22883`

**Original:** For common Content Manager panels and actions, Content Manager APIs are often more robust and better typed than injection zones.

**中文译文:** 如果目标是向 Content Manager 增加标准 action / panel，优先使用 Content Manager APIs；只有要插入某个特定 UI zone，而 Content Manager API 没有对应扩展点时，再使用 Injection Zones。

| 需求 | 推荐 API |
|---|---|
| Edit View side panel | `addEditViewSidePanel()` |
| Document action menu | `addDocumentAction()` |
| Edit View header action | `addDocumentHeaderAction()` |
| List View bulk action | `addBulkAction()` |
| 指定 plugin UI zone 插入任意 React component | `injectComponent()` |

**Original examples (kept unchanged):**

```js
app
  .getPlugin('content-manager')
  .apis
  .addDocumentAction(
    () => ({
      label:
        'Run custom action',
      onClick:
        ({ documentId }) =>
          runCustomAction(
            documentId
          ),
    })
  );

app
  .getPlugin('content-manager')
  .apis
  .addDocumentHeaderAction(
    () => ({
      label:
        'Open preview',
      onClick:
        ({ document }) =>
          openPreview(document),
    })
  );

app
  .getPlugin('content-manager')
  .apis
  .addBulkAction(
    () => ({
      label:
        'Bulk publish',
      onClick:
        ({ documentIds }) =>
          bulkPublish(
            documentIds
          ),
    })
  );

app
  .getPlugin('content-manager')
  .apis
  .addEditViewSidePanel([
    {
      name:
        'my-plugin.side-panel',
      Component:
        MySidePanel,
    },
  ]);

app
  .getPlugin('content-manager')
  .injectComponent(
    'editView',
    'right-links',
    {
      name:
        'my-plugin.custom-link',
      Component:
        MyCustomLink,
    }
  );
```
