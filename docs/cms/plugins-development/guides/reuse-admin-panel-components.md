# 📖 对照翻译：How to reuse built-in admin panel components in plugins

> Source: `docusaurus/docs/cms/plugins-development/guides/reuse-admin-panel-components.md`  
> Upstream SHA: `2bad444cf440e290f65230ba586be22945fd463b`

**Original:** Built-in admin components can be read from the component registry through `useStrapiApp`.

**中文译文:** Admin panel 内部部分 reusable React components 会注册到 app component registry。Plugin 可以使用 `useStrapiApp` 获取它们，避免重复实现 Strapi 已有 UI。

## Access the registry

```jsx
import {
  useStrapiApp,
} from '@strapi/admin/strapi-admin';

const components =
  useStrapiApp(
    'MyCustomComponent',
    (state) =>
      state.components
  );

const MediaLibraryDialog =
  components[
    'media-library'
  ];
```

**中文译文:** `useStrapiApp` 第一参数是 consumer label，主要用于错误提示；第二参数是 selector。

## Reuse Media Library dialog

| Prop | Required | 中文说明 |
|---|---:|---|
| `onSelectAssets` | Yes | 用户确认选择后接收完整 File[] |
| `onClose` | Yes | Dialog 关闭 callback |
| `initiallySelectedAssets` | No | 打开时预选的完整 Media Library asset objects |
| `allowedTypes` | No | 限制 files/images/videos/audios |
| `multiple` | No | 是否允许多选，默认 true |

**Original:** `initiallySelectedAssets` requires full asset objects, not only IDs.

**中文译文:** **不能只传 `id` / `name`。** Pre-selected assets 应使用 Upload API 返回的完整 Media Library asset shape。

```jsx
export function MyCustomComponent() {
  const [
    isOpen,
    setIsOpen,
  ] =
    useState(false);

  const components =
    useStrapiApp(
      'MyCustomComponent',
      (state) =>
        state.components
    );

  const MediaLibraryDialog =
    components[
      'media-library'
    ];

  const handleSelectAssets =
    (assets) => {
      console.log(
        'Selected assets:',
        assets
      );

      setIsOpen(false);
    };

  return (
    <>
      <button
        type="button"
        onClick={
          () =>
            setIsOpen(true)
        }
      >
        Open the Media Library
      </button>

      {isOpen && (
        <MediaLibraryDialog
          onSelectAssets={
            handleSelectAssets
          }
          onClose={
            () =>
              setIsOpen(false)
          }
        />
      )}
    </>
  );
}
```

**中文译文:** 同样的 component-registry 模式可用于其他被 Strapi admin 注册并公开的 built-in component。
