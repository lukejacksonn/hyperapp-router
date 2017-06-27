# HyperApp Router

Routing is the ability to move between different screens inside the same [HyperApp](https://github.com/hyperapp/hyperapp) application.

To add this functionality to your application, you can use `hyperapp-router` as a mixin.

```js
import { Router } from "hyperapp-router"
```

## Usage

```jsx
app({
  view: [
    ["/", (state, actions) => <h1>Home</h1>],
    ["/login", (state, actions) => <h1>Login</h1>],
    ["/:user", (state, actions) => <h1>Hi {state.router.params.user}</h1>],
    ["*", (state, actions) => <h1>404</h1>],
  ],
  mixins: [Router]
})
```

When the page loads or the browser fires a [popstate](https://developer.mozilla.org/en-US/docs/Web/Events/popstate) event, the first route that matches [location.pathname](https://developer.mozilla.org/en-US/docs/Web/API/Location) will be rendered.

Routes are matched in the order in which they are declared. To use the wildcard <samp>*</samp> correctly, it must be declared last.

|route                    | location.pathname    |
|-------------------------|-----------------------------------|
| <samp>/</samp>          | <samp>/</samp>
| <samp>/:foo</samp>      | Match <samp>[A-Za-z0-9]+</samp>. See [params](#params).
| <samp>*</samp>          | Match anything.

To navigate to a different route use [actions.router.go](#go).

## API

### state
#### params

Type: { <i>foo</i>: string, ... }

The matched route params.

|route                 |location.pathname    |state.router.params  |
|----------------------|---------------------|---------------------|
|<samp>/:foo</samp>    |/hyper               | { foo: "hyper" }    |

#### match

Type: string

The matched route.

### actions
#### go

Type: ([path](#router_go_path))
* path: string

Update [location.pathname](https://developer.mozilla.org/en-US/docs/Web/API/Location).

### events
#### route

Type: ([state](/docs/api.md#state), [actions](/docs/api.md#actions), [data](#events-data), [emit](/docs/api.md#emit)) | Array\<[route](#route)\>

* <a name="events-data"></a>data
  * [params](#params)
  * [match](#match)

Fired when a route is matched.
