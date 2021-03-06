---
title: Code Splitting
---

This feature splits your code into various bundles which are loaded on demand. It is used to achieve smaller bundles and control resource load prioritization which have a major impact on load time. To specify the splitting point you need to import modules in an asynchronous manner. To make it working with React, Falcon Client uses [async component](#async-components).

### Async components

Async components is based on [react-async-component](https://github.com/ctrlplusb/react-async-component)

It is highly recommended to have each page component asynchronous. Then page chunks do not impact themselves, as they contain only the necessary amount of code.

To convert React Component into a component which can be fetched on demand later, you need to wrap it with `asyncComponent` function:

```jsx
import { asyncComponent } from 'react-async-component';

const AsyncHome: asyncComponent({
  resolve: () => import('./src/pages/Home')
})

export default () => (
  <Switch>
    <Route exact path="/" component={AsyncHome} />
    {
      /// ...
    }
  </Switch>
)
```

For more information see [this](https://github.com/ctrlplusb/react-async-component)

### Vendors bundle

`vendors.js` is a chunk which combines only the common project dependencies into single file. As they should not change often, even between subsequent releases, it allows to turn on long term caching for rather big files.
