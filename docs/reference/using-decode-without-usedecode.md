## Using Decode without `useDecode`

If you do use any of the strategies below, [we'd definitely love to hear why](../contact).

If you'd prefer to make requests without using `useDecode`, you have a few options:

1. `useFetcher` + SWR

This can be helpful if for whatever reason you want to use SWR more directly:

```jsx
import { useFetcher } from "@decode/client";
import useSWR from "swr";

// ...

let fetcher = useFetcher();
let { data } = useSWR("listUsers", fetcher);
```

2. `useFetcher` on its own

Remember, you can use the fetcher to just make requests at any time:

```jsx
import { useFetcher } from "@decode/client";

// ...

let fetcher = useFetcher();

useEffect(() => {
  let doEffect = async () => {
    let data = await fetcher("listUsers");
  };
  doEffect();
});
```

3. `useToken` to use plain old fetch

Last, you can use `useToken` to grab an API token you can use to make a plain old fetch request:

```jsx
import { useToken } from "@decode/client";

// ...

let token = useToken();

useEffect(() => {
  let doEffect = async () => {
    let res = await fetch("https://api.usedecode.com/e/listJobs", {
      method: "POST",
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    if (!res.ok) {
      setError("Uh oh, something went wrong when fetching that request.");
    }
    let json = await res.json();
    let data = res.result;
  };
  doEffect();
});
```
