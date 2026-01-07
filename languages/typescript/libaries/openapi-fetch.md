# openapi-fetch

[openapi-fetch](https://openapi-ts.dev/openapi-fetch/) is a TypeScript library that provides a strongly-typed fetch client generated from your OpenAPI schema. It enables type-safe API calls and seamless integration with tools like React Query, improving developer experience and reducing runtime errors. At BBI we use it in our frontend applications to generate types from our FastAPI applications.

## Installation

Install the required packages:

```sh
npm install openapi-typescript openapi-fetch openapi-react-query
```

### Generating Types from OpenAPI

Add a script to your `package.json` to generate TypeScript types from your OpenAPI schema. Replace the URL with the location of your FastAPI (or other) OpenAPI endpoint:

```json
{
    // ...existing package.json fields
    "scripts": {
        // ...existing scripts
        "types": "npx openapi-typescript http://localhost:8000/openapi.json -o ./src/lib/api/v1.d.ts"
    }
}
```

Run the following command to generate the types:

```sh
npm run types
```

This will create or update the `./src/lib/api/v1.d.ts` file with types based on your OpenAPI schema.

### Setting up the API Client

To use the fetch client or React Query client, create a file at `./src/lib/api/client.ts`:

```ts
import createFetchClient, { type Middleware } from "openapi-fetch"
import createClient from "openapi-react-query"
import type { paths } from "@/lib/api/v1"

const client = createFetchClient<paths>({
    baseUrl: import.meta.env.VITE_BACKEND_URL,
    credentials: "include",
    headers: {
        "Content-Type": "application/json",
    },
})

// Optional: Add middleware for handling authentication errors
const middleware: Middleware = {
    onResponse: async ({ request, response }) => {
        if (UNPROTECTED_PATHS.some((path) => request.url.endsWith(path))) {
            return undefined
        }
        if (response.status === 401) {
            await useAuthStore.getState().signout()
            window.location.href = "/signin"
        }
    },
}

client.use(middleware)

const query = createClient(client)

export { client, query }
```

### Usage Examples

#### Using the Fetch Client (e.g., in a loader)

```ts
export const Route = createFileRoute("/todos")({
    component: RouteComponent,
    loader: async () => {
        const { data, error } = await client.request("get", "/todos")
        if (error) {
            throw new Error("Failed to fetch todos")
        }
        return { todos: data }
    },
})
```

#### Using the React Query Client (e.g., in a component)

```ts
const { mutate: createTodo, isPending } = query.useMutation("post", "/todos")
```
