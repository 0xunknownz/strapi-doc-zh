# 📖 对照翻译：Admin Panel API — Redux store & reducers

> Source: `docusaurus/docs/cms/plugins-development/admin-redux-store.md`  
> Upstream SHA: `17ad08918aec6ce577349f82e447f416ee62220c`

**Original:** Add custom reducers during `register`, then use React Redux hooks to read, update, and subscribe to admin state.

**中文译文:** Strapi admin panel 使用全局 Redux store 管理 application state。Plugin 可以：
- 在 `register()` 中注册 custom reducer；
- 用 `useSelector` 读取 state；
- 用 `useDispatch` dispatch action；
- 用 `useStore` 获取 store instance 并订阅变化。

## Store overview

**Original:** The store includes `admin_app`, `adminApi`, and plugin-specific slices.

**中文译文:** 主要 slices：
- `admin_app`：theme、language、permissions、authentication token；
- `adminApi`：RTK Query admin endpoint state；
- Plugin custom reducers。

## Add custom reducers

```js
import {
  exampleReducer,
} from './reducers';

import pluginId
  from './pluginId';

const reducers = {
  [
    `${pluginId}_exampleReducer`
  ]:
    exampleReducer,
};

export default {
  register(app) {
    app.addReducers(
      reducers
    );
  },
};
```

**中文译文:** Reducer name 建议带 plugin prefix，避免与其他 plugin / core slice 冲突。

## Read state with `useSelector`

```jsx
import {
  useSelector,
} from 'react-redux';

const currentTheme =
  useSelector(
    (state) =>
      state.admin_app
        ?.theme
        ?.currentTheme
  );

const currentLocale =
  useSelector(
    (state) =>
      state.admin_app
        ?.language
        ?.locale
  );

const isAuthenticated =
  useSelector(
    (state) =>
      !!state.admin_app
        ?.token
  );
```

## Common `admin_app` state

| Property | 中文说明 |
|---|---|
| `theme.currentTheme` | `light` / `dark` / `system` |
| `theme.availableThemes` | 可选 theme list |
| `language.locale` | 当前 admin locale |
| `language.localeNames` | Locale code → display name |
| `token` | Admin authentication token |
| `permissions` | 当前 user permissions |

**Original:** Internal store shape may change; plugins should avoid depending on undocumented state.

**中文译文:** Core Redux state 属于 admin implementation details 的一部分。只有文档明确公开的字段才应作为 plugin dependency；不要耦合 undocumented internal shape。

## Dispatch actions

```jsx
import {
  useDispatch,
} from 'react-redux';

const dispatch =
  useDispatch();

dispatch({
  type:
    'admin/setAppTheme',
  payload:
    'dark',
});

dispatch({
  type:
    'admin/setLocale',
  payload:
    'fr',
});
```

**Original:** Plugins usually should dispatch to their own reducers instead of mutating global admin state.

**中文译文:** 上例演示 core action；实际 plugin 应优先维护自己的 slice，避免无必要地改变整个 admin panel theme / locale / auth state。

## Core action examples

| Action | Payload | 中文说明 |
|---|---|---|
| `admin/setAppTheme` | string | 修改 theme |
| `admin/setAvailableThemes` | string[] | 修改可用 themes |
| `admin/setLocale` | string | 修改 admin locale |
| `admin/setToken` | string/null | 设置 auth token |
| `admin/login` | `{ token, persist? }` | Login |
| `admin/logout` | void | Logout |

**中文译文:** Redux Toolkit action type 使用 `sliceName/actionName` 格式，因此 admin slice action 以 `admin/` 开头。

## Access store instance

```jsx
import {
  useStore,
} from 'react-redux';

import {
  useEffect,
} from 'react';

const App = () => {
  const store =
    useStore();

  useEffect(() => {
    const unsubscribe =
      store.subscribe(
        () => {
          const state =
            store.getState();

          console.log(
            state.admin_app
              ?.theme
              ?.currentTheme
          );
        }
      );

    return () =>
      unsubscribe();
  }, [store]);

  return (
    <div>
      My Plugin
    </div>
  );
};
```

**中文译文:** 手工 subscription 必须在 React effect cleanup 中 unsubscribe，否则会产生 memory leak。

## Best practices

**中文译文:**
- 读取 state 优先 `useSelector`，让 React 自动 re-render；
- Subscription 必须 cleanup；
- 为 plugin 自己的 `RootState` / `AppDispatch` 建立 local typings；
- Strapi admin utility 从官方 documented package path import；
- 只在确实需要时 dispatch；
- 尽量不要修改 core admin global state；
- 复杂 plugin state 使用自己的 reducer slice。
