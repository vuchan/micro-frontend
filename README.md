[中文](./README-zh_CN.md) | English

# micro-frontend
✨🌟✨ A single-SPA solution for frontend, use it only need to learn 3 APIs in 3 minutes.

+ Use multiple projects on the same page without refreshing the page.
+ Write code using a new project, without rewriting your existing app.
+ Lazy load code for improved initial load time with Webpack Code-Splitting.


## Usage
+ step one: Create an host object.

*[frontend-host project](./demo/frontend-host/src/main.js)*
```js
// ...
import app1 from '../../frontend-1/src/main'
import app2 from '../../frontend-2/src/main'
import microfe from 'micro-frontend'

const host = microfe.createHost() // 1

host.createApp({ // 2
  path: '/',
  render() {/*  */}
  // if Vue: new Vue({ render: h => h(App) }).$mount('#app')
  // if React: ReactDOM.render(<App />, document.querySelector('#app'))
  // if Angular: ??
})
host.createApp(app1)
host.createApp(app2)

host.start() // 3
```

+ step two: Register each child app to the host object:

*[forntend-1 project](./demo/frontend-1/src/main.js)*
```js
// ...
const host = microfe.createHost()
const app = {
  path: '/demo1',
  render() {/* your render code*/}
}

host.createApp(app) // The same app reference or app.path will be called only once too.

/* if u wanna run this child project single, open following code */
// host.start()
export default app;
```

*[forntend-2 project](./demo/frontend-1/src/main.js)*
```js
// ...
const host = microfe.createHost() // it is a singleton object, so don't worry how many times it be called.
const app = {
  path: '/demo1',
  render() {/* your render code*/}
}

host.createApp(app) // The same app reference or app.path will be called only once too.

/* if u wanna run this child project single, open following code */
// host.start()
export default app;
```

more and more ...

+ step three: Run the host project which one u called `host.start()` method.


## TODO
+ [ ] Supports any frontend framework, Angular ??
+ [ ] lazy load each child app's entry component
+ [ ] build each child app independent and separately


## Questions
The following questions i am not very clear yet or no any good idea about them.

+ how to manage common dependencies of each child app?
+ how to deploy them? Only deploy host project or every portal project? Or a middle layer server?


## Troubleshooting
+ if you met one error like this `Error: No ESLint configuration found.` when you run this project, may this link [github issue](https://github.com/vuejs/vue-cli/issues/2539) can help you.

```js
INFO  Starting development server... 94% after seal

ERROR  Failed to compile with 1 errors

Module build failed (from ./node_modules/_eslint-loader@2.1.1@eslint-loader/index.js):
  Error: No ESLint configuration found.    at Config.getLocalConfigHierarchy
```
