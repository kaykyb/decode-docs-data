# useFetcher

Decode also supports making one-off requests with `useFetcher`. You use a fetcher function whenever you want to make _write_ requests through Decode.

Grab a fetcher function near the top of your component:

```jsx
const App = () => {
  let fetcher = useFetcher()
  // ...
```

Then you can perform the request in any handler function within your component, like this:

```jsx
let handleButtonClick = () => {
  fetcher("incrementCounter");
};
```
