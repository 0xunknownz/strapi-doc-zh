# 📖 对照翻译：Content Manager APIs

> Source: `docusaurus/docs/cms/plugins-development/content-manager-apis.md`  
> Upstream SHA: `d9108c47dc45ea995b082dd104edfc4e17579384`

**Original:** Content Manager APIs let plugins add panels, actions, bulk actions, and custom rich-text blocks to the Content Manager.

**中文译文:** Content Manager APIs 属于 Admin Panel API，允许 plugin 在 Content Manager 中增加 side panel、document action、header action、bulk action，以及自定义 Blocks editor block type。

**Original:** The APIs are available through `app.getPlugin('content-manager').apis`.

**中文译文:** 这些 API 统一从：

`app.getPlugin('content-manager').apis`

获取。

**Original:** In TypeScript, `apis` is typed as `unknown`; cast it to `ContentManagerPlugin['config']['apis']`.

**中文译文:** TypeScript 中 `apis` 当前会被推断为 `unknown`，应显式 cast：

```ts
import type {
  ContentManagerPlugin,
} from '@strapi/content-manager/strapi-admin';

const apis =
  app.getPlugin('content-manager').apis
    as ContentManagerPlugin['config']['apis'];
```

## Shared API shape

**Original:** Each API accepts either an array of components or a reducer function receiving the current list.

**中文译文:** 大多数 API 支持两种调用方式：
- 直接传 component/action array，追加内容；
- 传 reducer function，接收当前 items 并返回新 array，可控制插入位置。

```js
apis.addEditViewSidePanel([
  ReleasesPanel,
]);

apis.addEditViewSidePanel(
  (panels) => [
    SuperImportantPanel,
    ...panels,
  ]
);
```

## Context objects

### ListViewContext

```ts
interface ListViewContext {
  collectionType: string;
  documents: Document[];
  model: string;
}
```

**中文译文:** List View extension 可以读取当前 content-type、已选 documents 和 model UID。

### EditViewContext

```ts
interface EditViewContext {
  activeTab:
    | 'draft'
    | 'published'
    | null;

  collectionType: string;
  document?: Document;
  documentId?: string;
  meta?: DocumentMetadata;
  model: string;
}
```

**中文译文:** 创建新 entry 时 `document` / `documentId` / `meta` 可能为 `undefined`；未启用 Draft & Publish 时 `activeTab` 为 `null`。

## `addEditViewSidePanel()`

**Original:** Adds custom panels to the Edit View sidebar.

**中文译文:** 在 Edit View 侧边栏加入自定义 panel。

```tsx
type PanelComponent =
  (
    props:
      PanelComponentProps
  ) => ({
    title: string;
    content:
      React.ReactNode;
  });
```

```jsx
const Panel = ({
  activeTab,
}) => ({
  title: 'My Panel',
  content:
    <p>
      I'm on {activeTab}
    </p>,
});
```

## `addDocumentAction()`

**Original:** Adds document-level actions that can appear in several positions.

**中文译文:** 添加单 document action，可显示在：
- `panel`
- `header`
- `table-row`
- `preview`
- `relation-modal`

常用 description fields：
- `label`
- `onClick`
- `icon`
- `disabled`
- `position`
- `dialog`
- `variant`
- `loading`

**Original:** Actions can open dialog, notification, or modal UI.

**中文译文:** `dialog` 可以声明：
- Confirmation dialog；
- Notification；
- Custom modal。

## `addDocumentHeaderAction()`

**Original:** Adds prominent actions to the Edit View header.

**中文译文:** 在 Edit View 标题区域增加快速 action，可定义：
- `label`
- `icon`
- `type: 'icon' | 'default'`
- `onClick`
- `dialog`
- `options`
- `onSelect`
- `value`

适合 Preview、external workflow、quick operation 等。

## `addBulkAction()`

**Original:** Adds actions shown when documents are selected in List View.

**中文译文:** 当 List View 选中一个或多个 documents 时显示 bulk action，例如 Add to Release、Bulk publish、自定义 export 等。

```ts
interface BulkActionDescription {
  dialog?: DialogOptions
    | NotificationOptions
    | ModalOptions;

  disabled?: boolean;
  icon?: React.ReactNode;
  label: string;
  onClick?:
    (
      event:
        React.SyntheticEvent
    ) => void;

  type?:
    | 'icon'
    | 'default';

  variant?:
    ButtonProps['variant'];
}
```

## `addRichTextBlocks()`

**Original:** Registers custom block types for the Blocks rich text editor.

**中文译文:** `addRichTextBlocks()` 用于扩展 **Blocks** rich-text field，为 Slate-based editor 注册新的 block type。

**Original:** It must run during `register()`, not `bootstrap()`.

**中文译文:** **必须在 `register()` lifecycle 调用**，因为 Blocks editor 的 Slate instance 在这个阶段初始化。

### Add a block

```jsx
app
  .getPlugin(
    'content-manager'
  )
  .apis
  .addRichTextBlocks({
    callout: {
      renderElement:
        (props) =>
          <Callout
            {...props.attributes}
          >
            {props.children}
          </Callout>,

      icon:
        Information,

      label: {
        id:
          'my-plugin.blocks.callout',
        defaultMessage:
          'Callout',
      },

      matchNode:
        (node) =>
          node.type ===
            'callout',

      isInBlocksSelector:
        true,

      snippets:
        [':::callout'],
    },
  });
```

### Transform the current block store

**Original:** Passing a function can replace or remove built-in blocks.

**中文译文:** Function form 接收当前 blocks store，因此可以删除 / 替换 built-in block：

```js
apis.addRichTextBlocks(
  (currentBlocks) => {
    const {
      code:
        _removed,
      ...rest
    } =
      currentBlocks;

    return rest;
  }
);
```

## Block definition

| Property | Required | 中文说明 |
|---|---:|---|
| `renderElement` | Yes | React renderer |
| `matchNode` | Yes | 判断 Slate node 是否属于该 block |
| `isInBlocksSelector` | No | 是否出现在 toolbar dropdown |
| `icon` | 条件必需 | Selector 中显示的 icon |
| `label` | 条件必需 | Localized label |
| `handleConvert` | No | 用户选择 block type 时转换 node |
| `handleEnterKey` | No | 自定义 Enter |
| `handleBackspaceKey` | No | 自定义 Backspace |
| `handleTab` | No | 自定义 Tab |
| `handleShiftTab` | No | 自定义 Shift+Tab |
| `snippets` | No | 输入 shortcut 后按 Space 自动转换 |
| `dragHandleTopMargin` | No | Drag handle vertical offset |
| `plugin` | No | Slate plugin |
| `isDraggable` | No | 控制 element 是否可 drag |

**Original:** Built-in block keys include paragraph, heading-one through heading-six, ordered/unordered lists, image, quote, code, link, and list-item.

**中文译文:** 修改内置 blocks 前应使用其稳定 key，例如 `paragraph`、`heading-one`、`list-ordered`、`image`、`quote`、`code`、`link` 等。
