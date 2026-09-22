# 📖 对照翻译：How to create components for Strapi plugins

> Source: `docusaurus/docs/cms/plugins-development/guides/create-components-for-plugins.md`  
> Upstream SHA: `4937459961269a461be06b0aad3fe4d9ad05eb30`

**Original:** Create reusable Strapi components for plugins either through Content-Type Builder or manually from schema files.

**中文译文:** Plugin 可以像普通 Strapi project 一样定义 reusable component data structure。推荐通过 Content-Type Builder 创建，也可以手工编写 component schema。

## Recommended: Content-Type Builder

**Original:** Use Content-Type Builder for the normal component creation flow.

**中文译文:** 最推荐的方式是在 admin panel 中使用 [Content-Type Builder](/cms/features/content-type-builder#new-component)，这样 schema structure、field validation 与 UI metadata 都由 Strapi 管理。

## Manual component creation

**中文译文:** 手工方式一般需要：
1. 在 plugin server structure 中创建 component schema；
2. 确保 component 被 plugin 正确注册；
3. 在 plugin content-type schema 中通过 component UID 引用。

### Component field example

```json
{
  "attributes": {
    "myComponent": {
      "type": "component",
      "repeatable": true,
      "component": "category.componentName"
    }
  }
}
```

### Component schema example

```json title="my-plugin/server/components/my-category/my-component.json"
{
  "collectionName":
    "components_my_category_my_components",

  "info": {
    "displayName":
      "My Component",
    "icon":
      "align-justify"
  },

  "attributes": {
    "name": {
      "type":
        "string",
      "required":
        true
    },

    "description": {
      "type":
        "text"
    }
  }
}
```

**中文译文:** Component 最终可被多个 plugin content-types 复用。如果对应 content-type 的 `pluginOptions` 允许 Content Manager / Content-Type Builder visibility，组件也会在 admin UI 中正常出现。
