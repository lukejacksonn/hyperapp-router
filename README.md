# hyperapp-router

Routing is the ability to move between different screens inside the same application.

To add this functionality to your application, you can use `hyperapp-router` as a plugin.

```js
import { Router } from "hyperapp-router"
```

## <a name="router"></a> Router

The router selects a view whose key matches the value of [location.pathname](https://developer.mozilla.org/en-US/docs/Web/API/Location) and updates the current view before it is rendered.

To associate views with keys, use the [view](/hyperapp/hyperapp/wiki/Application#view) property as a dictionary where the _key_ is the route and the _value_ is the view function.

* `*` Use to match when no other route matches.
* `/` Use to match the index route.
* `/:key` Use to match a route using the regular expression [A-Za-z0-9]+. The matched params are stored in [model.router.params](#router_params).

### <a name="router_go"></a> actions.router.go

Sets the [location.pathname](https://developer.mozilla.org/en-US/docs/Web/API/Location) to the given path. If the path matches an existing route, the corresponding view will be rendered.

Signature: (path).

<a name="cb1"></a> <sub>[View Online](https://hyperapp-router-go.glitch.me)</sub>

```jsx
app({
  view: {
    "/": (model, actions) =>
      <div>
        <h1>Home</h1>
        <button
          onClick={_ => actions.router.go("/about")}>
          About
        </button>
      </div>,

    "/about": (model, actions) =>
      <div>
        <h1>About</h1>
        <button
          onClick={_ => actions.router.go("/")}>
          Home
        </button>
      </div>
  },
  plugins: [Router]
})
```

### <a name="router_match"></a> model.router.match

Stores the matched route.

<table>
  <th>Route</th>
  <th colspan=3>URL</th>

  <tr>
    <td>*</td>
    <td>/foo</td>
    <td>/foo/bar/baz</td>
  </tr>

  <tr>
    <td>/:key</td>
    <td>/foo</td>
    <td>/bar</td>
  </tr>

  <tr>
    <td>/item/:id</td>
    <td>/item/7a45</td>
    <td>/item/1c63</td>
  </tr>

  <tr>
    <td>/user/:name/post/:id</td>
    <td>/user/hyper/post/9df0</td>
    <td>/user/app/post/5ag1</td>
  </tr>
</table>

### <a name="router_params"></a> model.router.params

Stores the matched route params.

<table>
  <th>Route</th>
  <th>URL</th>
  <td><i>params</i>.<b>name</b></td>
  <td><i>params</i>.<b>id</b></td>

  <tr>
    <td>/user/:name/post/:id</td>
    <td>/user/hyper/post/9df0</td>
    <td>hyper</td>
    <td>9df0</td>
  </tr>

  <tr>
    <td>/user/:name/post/:id</td>
    <td>/user/app/post/5ag1</td>
    <td>app</td>
    <td>5ag1</td>
  </tr>
</table>
