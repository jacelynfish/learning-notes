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



