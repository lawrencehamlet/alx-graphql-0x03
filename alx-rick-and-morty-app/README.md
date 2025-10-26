This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/pages/api-reference/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.tsx`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/pages/building-your-application/routing/api-routes) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.ts`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/pages/building-your-application/routing/api-routes) instead of React pages.

This project uses [`next/font`](https://nextjs.org/docs/pages/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn-pages-router) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/pages/building-your-application/deploying) for more details.

## GraphQL: Get a specific character by ID

This folder contains example GraphQL queries to fetch a single character from the Rick and Morty GraphQL API and saved sample outputs.

Endpoint: https://rickandmortyapi.com/graphql

Files added:

- `character-id-1.graphql` — query for character with id 1
- `character-id-1-output.json` — sample JSON response for id 1
- `character-id-2.graphql` — query for character with id 2
- `character-id-2-output.json` — sample JSON response for id 2
- `character-id-3.graphql` — query for character with id 3
- `character-id-3-output.json` — sample JSON response for id 3
- `character-id-4.graphql` — query for character with id 4
- `character-id-4-output.json` — sample JSON response for id 4

Each `.graphql` file contains a single query using the `character(id: ID!)` field and requests the following fields: `id`, `name`, `status`, `species`, `type`, `gender`.

Run the queries using curl or PowerShell. Example (PowerShell):

```
Invoke-RestMethod -Uri 'https://rickandmortyapi.com/graphql' -Method Post -Body (@{query='query { character(id:1) { id name status species type gender } }'} | ConvertTo-Json) -ContentType 'application/json'
```

### GraphQL: Get a paginated list of characters

The repository also includes example queries for fetching paginated lists of characters using `characters(page: Int)`. Each query selects the `id`, `name`, `status`, and `image` fields and returns `info` and `results`.

Files added for pagination:

- `characters-page-1.graphql` — query for page 1
- `characters-page-1-output.json` — sample response (subset of results)
- `characters-page-2.graphql` — query for page 2
- `characters-page-2-output.json` — sample response (subset of results)
- `characters-page-3.graphql` — query for page 3
- `characters-page-3-output.json` — sample response (subset of results)
- `characters-page-4.graphql` — query for page 4
- `characters-page-4-output.json` — sample response (subset of results)

PowerShell example to fetch page 1:

```
Invoke-RestMethod -Uri 'https://rickandmortyapi.com/graphql' -Method Post -Body (@{query='query { characters(page:1) { info { count pages } results { id name status image } } }'} | ConvertTo-Json) -ContentType 'application/json'
```

Or with curl:

```
curl -s -X POST https://rickandmortyapi.com/graphql -H "Content-Type: application/json" -d "{\"query\":\"query { characters(page:1) { info { count pages } results { id name status image } } }\"}"
```
