# 📖 对照翻译：Use `locale` with the GraphQL API

> Source: `docusaurus/docs/cms/api/graphql/locale.md`  
> Upstream SHA: `39a1be494cf58fedb1089d72f59be98eb881e29d`

**Original:** Use the `locale` argument with the GraphQL API to query, create, update, and delete documents for a specific locale.

**中文译文:** 启用 Internationalization 后，GraphQL schema 会包含 `locale` field / argument。可以通过 `locale` 查询、创建、更新、删除特定 localization。

## Fetch all documents in a locale

**Original:** Pass `locale` to the collection query.

```graphql
query {
  restaurants(locale: "fr") {
    documentId
    name
    locale
  }
}
```

**中文译文:** 上例只返回 French locale 中存在的 restaurant documents。

## Fetch one document in a locale

**Original:** Pass both `documentId` and `locale`.

```graphql
query Restaurant(
  $documentId: ID!,
  $locale: I18NLocaleCode
) {
  restaurant(
    documentId: "a1b2c3d4e5d6f7g8h9i0jkl",
    locale: "fr"
  ) {
    documentId
    name
    description
    locale
  }
}
```

**中文译文:** `documentId` 标识逻辑 document；`locale` 决定返回该 document 的哪一个 localization。

## Create a localized document

**Original:** Pass `locale` to the create mutation.

```graphql
mutation CreateRestaurant(
  $data: RestaurantInput!,
  $locale: I18NLocaleCode
) {
  createRestaurant(
    data: {
      name: "Brasserie Bonjour",
      description: "Description in French goes here"
    },
    locale: "fr"
  ) {
    documentId
    name
    description
    locale
  }
}
```

**中文译文:** 该 mutation 直接在 `fr` locale 中创建 Restaurant document。

## Update a specific locale

**Original:** Pass `documentId`, `data`, and `locale` to update one localization.

```graphql
mutation UpdateRestaurant(
  $documentId: ID!,
  $data: RestaurantInput!,
  $locale: I18NLocaleCode
) {
  updateRestaurant(
    documentId: "a1b2c3d4e5d6f7g8h9i0jkl"
    data: {
      description: "New description in French"
    },
    locale: "fr"
  ) {
    documentId
    name
    description
    locale
  }
}
```

**中文译文:** 只更新该 document 的 French localization，不影响其他 locales。

## Delete a localization

**Original:** Pass `locale` to delete a specific locale version.

```graphql
mutation DeleteRestaurant(
  $documentId: ID!,
  $locale: I18NLocaleCode
) {
  deleteRestaurant(
    documentId: "xzmzdo4k0z73t9i68a7yx2kk",
    locale: "fr"
  ) {
    documentId
  }
}
```

**中文译文:** 该 mutation 只删除指定 document 的 `fr` localization。
