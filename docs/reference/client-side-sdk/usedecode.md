# useDecode

Underneath the hood, `useDecode` wraps the SWR library. You can find the docs for SWR here:

📔[https://github.com/vercel/swr](https://github.com/vercel/swr)

So, if you know how to do something with SWR, you can probably do it with `useDecode`!

The key difference: You pass in an endpoint and a `fetcher` function to SWR, like so:

```jsx
let { data, error } = useSWR("/api/users", fetcher);
```

Whereas all you need to pass to `useDecode` is a slug, like so:

```jsx
let { data, error } = useDecode("getUser");
```

In addition, you can _optionally_ pass in a "transform" function, like this:

```jsx
import camelcaseKeys from "camelcase-keys";

// ...

let { data, error } = useDecode("getUser", camelcaseKeys);
```

The transform function runs after the results are received from Decode but before they are cached by SWR. So, the data is in its "post transformation" state throughout your React app.

Put another way, this is the pipeline:

```bash
fetched from decode
|> transformed by transform function
|> cached and returned
```
