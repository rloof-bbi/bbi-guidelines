# TanStack Router

[TanStack Router](https://tanstack.com/router/latest/docs/framework/react/quick-start) is a powerful, type-safe router for React applications. It is designed for modern Single Page Applications (SPAs) and provides a file-based routing experience, excellent developer ergonomics, and first-class TypeScript support. TanStack Router is ideal for frontend projects that require robust routing, code-splitting, and data loading.

## Installation

Follow the official quick start to scaffold a new project:

```sh
npx create-tsrouter-app@latest
```

You will be prompted for several options:

-   **Project name:** This will also be the directory name.
-   **File router:** Yes
-   **Tailwind:** Yes
-   **Select toolchain:** None (press Enter)
-   **Add-ons:** None (press Enter)
-   **Examples:** None (press Enter)

Once the project is created, open it in VS Code and start the development server:

```sh
npm run dev
```

## Project Structure

After setup, your project will have a structure similar to:

```
.
├── .tanstack/              # Auto-generated router files
├── node_modules/           # Dependencies
├── public/                 # Static assets
├── src/                    # Source code
│   ├── components/         # Reusable React components
│   ├── hooks/              # Custom React hooks
│   ├── lib/                # Utility libraries (e.g., API clients)
│   ├── routes/             # Route definitions (file-based routing)
│   ├── main.tsx            # App entry point
│   ├── reportWebVitals.ts  # (auto-generated)
│   ├── routeTree.gen.ts    # (auto-generated)
│   └── styles.css          # Global styles
├── .env                    # Environment variables (see .env.sample)
├── .env.sample             # Environment variable template
├── .gitignore              # Git ignore rules
├── index.html              # HTML entry point
├── package-lock.json       # (auto-generated)
├── package.json            # (auto-generated)
├── README.md               # (auto-generated)
├── tsconfig.json           # TypeScript config
└── vite.config.ts          # Vite config
```

## Guidelines

-   For API integration, we use [openapi-fetch](https://openapi-ts.dev/openapi-fetch/). See the [openapi-fetch guidelines](./openapi-fetch.md) for setup and usage details.
-   Use lowercase, kebab-case for route files/folders (e.g., `user-profile.tsx`).
-   Use camelCase for variable and function names (e.g., `userProfile`, `fetchTodos`).
-   Keep routes simple and make use of components.
-   Use layout routes for shared UI and authentication (e.g., protect routes by wrapping them in an auth layout).

## Deployment

When you build your TanStack Router project, the result is a set of static files that can be deployed to any static hosting provider. Our preferred platform is **Azure Static Web Apps**, which offers easy integration with CI/CD and global distribution.

To build your project for production:

```sh
npm run build
```

The output will be in the `dist/` directory, ready for deployment.
