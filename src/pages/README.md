# 路由系统

基于Pages文件的路由系统，默认`/src/pages/`目录下的vue或md文件将自动生成可用的route

## File-based Routing

Routes will be auto-generated for Vue files in this dir with the same file structure.
Check out [`vite-plugin-pages`](https://github.com/hannoeru/vite-plugin-pages) for more details.

### Path Aliasing

`~/` is aliased to `./src/` folder.

For example, instead of having

```ts
import { isDark } from '../../../../composables'
```

now, you can use

```ts
import { isDark } from '~/composables'
```

### Basic Routing

Pages will automatically map files from your pages directory to a route with the same name:

- `src/pages/users.vue` -> `/users`
- `src/pages/users/profile.vue` -> `/users/profile`
- `src/pages/settings.vue` -> `/settings`

### Index Routes

Files with the name index are threated as the index page of a route:

- `src/pages/index.vue` -> `/`
- `src/pages/users/index.vue` -> `/users`

### Dynamic Routes

> 动态路由

Dynamic routes are denoted using square brackets. Both directories and pages can be dynamic:

- `src/pages/users/[id].vue` -> `/users/:id` (`/users/one`)
- `src/pages/[user]/settings.vue` -> `/:user/settings` (`/one/settings`)

Any dynamic parameters will be passed to the page as props. For example, given the file `src/pages/users/[id].vue`, the route `/users/abc` will be passed the following props:

```{ "id": "abc" }```

### Nested Routes

> 嵌套路由

We can make use of Vue Routers child routes to create nested layouts. The parent component can be defined by giving it the same name as the directory that contains your child routes.

For example, this directory structure:

```text
src/pages/
  ├── users/
  │  ├── [id].vue
  │  └── index.vue
  └── users.vue
```

will result in this routes configuration:

```json
[
  {
    "path": "/users",
    "component": "/src/pages/users.vue",
    "children": [
      {
        "path": "",
        "component": "/src/pages/users/index.vue",
        "name": "users"
      },
      {
        "path": ":id",
        "component": "/src/pages/users/[id].vue",
        "name": "users-id"
      }
    ]
  }
]
```

### Catch-all Routes

> 匹配不存在的路由

Catch-all routes are denoted with square brackets containing an ellipsis:

- `src/pages/[...all].vue` -> `/*` (`/non-existent-page`)

The text after the ellipsis will be used both to name the route, and as the name of the prop in which the route parameters are passed.
