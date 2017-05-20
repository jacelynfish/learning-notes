## Server-side rendering

#### Data Reactivity

Data reactivity is disabled by default: The rendering process needs to be deterministic, which means the application state will already be resolved when reandering starts.



#### Component lifecycle hook

Only `beforeCreate` and `created` will be called during SSR.

_**Vue instance lifecycle diagram**_

![lifecycle](https://vuejs.org/images/lifecycle.png)

#### Access platform-specific APIs

* Wrap platform-specific implementations inside a universal API
* Lazily access browser-only APIs inside client-only lifecycle hooks



#### Avoid stateful singleton

Expose a factory function to repeatedly create fresh app instances for each request; the same rules apply to router, store and event bus as well.

```javascript
//app.js
const Vue = require('vue')

module.exports = function createApp (context) {
  return new Vue({
    data: {
      url: context.url
    },
    template: `<div>The visited URL is: {{ url }}</div>`
  })
}
```

```javascript
// server.js
const createApp = require('./app')

server.get('*', (req, res) => {
  const context = { url: req.url }
  const app = createApp(context)

  renderer.renderToString(app, (err, html) => {
    // handle error...
    res.end(html)
  })
})
```



#### Build steps with Webpack

**Server entry**: required by the server and used for SSR

**Client entry**: required by the brower to hydrate the static markup

![](https://cloud.githubusercontent.com/assets/499550/17607895/786a415a-5fee-11e6-9c11-45a2cfdf085c.png)

#### Code structure

```shell
src
├── components
│   ├── Foo.vue
│   ├── Bar.vue
│   └── Baz.vue
├── App.vue
├── app.js # universal entry
├── entry-client.js # runs in browser only
└── entry-server.js # runs on server only
```

##### `app.js`

only used as a factory to create new vue instances

```javascript
import Vue from 'vue'
import App from './App.vue'

// export a factory function for creating fresh app, router and store
// instances
export function createApp () {
  const app = new Vue({
    // the root instance simply renders the App component.
    render: h => h(App)
  })
  return { app }
}
```

##### `entry-client.js`

creates the app and mounts it to the DOM

```javascript
import { createApp } from './app'

// client-specific bootstrapping logic...

const { app } = createApp()

// this assumes App.vue template root element has id="app"
app.$mount('#app')
```

##### `entry-server.js`

```javascript
import { createApp } from './app'

export default context => {
  const { app } = createApp()
  return app
}
```



#### Code-Splitting

Employing Webpack 2's code splitting mechanism to achieve asynchronous requests for components may have some limitations in both SSR and client-side SPA. We need to resolve all the async components upfront on the server before starting the render, because otherwise we will just get empty placeholders in the markup. On the client, we also need to do this before starting hydration. Otherwise the client will run into content mismatch.

But it works perfectly at route level: `vue-router` will automatically resolve matched async components when resolving a route. **What you need to do is make sure to use `router.onReady` on both server and client. **

```javascript
// entry-server.js
import { createApp } from './app'

export default context => {
  // since there could potentially be asynchronous route hooks or components,
  // we will be returning a Promise so that the server can wait until
  // everything is ready before rendering.
  return new Promise((resolve, reject) => {
    const { app, router } = createApp()

    // set server-side router's location
    router.push(context.url)

    // wait until router has resolved possible async components and hooks
    router.onReady(() => {
      const matchedComponents = router.getMatchedComponents()
      // no matched routes, reject with 404
      if (!matchedComponents.length) {
        reject({ code: 404 })
      }

      // the Promise should resolve to the app instance so it can be rendered
      resolve(app)
    }, reject)
  })
}
```



#### Router related APIs

This is from `vue-router`

- **router.getMatchedComponents(location?)**

  Returns an _Array of the components_ (definition/constructor, not instances) matched by the provided location or the current route. 

- **router.onReady(callback, [errorCallback])**

  This method queues a callback to be called when the router has completed the _**initial** navigation_, which means it has resolved all _async enter hooks and async components that are associated with the **initial** route_.

  The second argument `errorCallback` is only supported in 2.4+. It will be called when the initial route resolution runs into an error (e.g. failed to resolve an async component).