# Technical Report

## Rendering Strategy Rationale

- Home: SSG for fast initial load and global cacheability. Client search/filter enables interactivity without revalidation. `revalidate = false` ensures true static output.
- Product Detail: ISR to serve mostly-static content with periodic freshness. `revalidate = 60` balances freshness and performance. `generateStaticParams` prebuilds all product pages.
- Dashboard: SSR with `dynamic = 'force-dynamic'` for real-time inventory and valuation metrics on each request.
- Admin: CSR to isolate admin-only interactivity, client state, and form workflows.
- Recommendations: Server components for data fetch and rendering; client button for wishlist interactivity.

## Data Flow Architecture

- UI pages call server utilities in `lib/products` when using server components (Home, Product Detail, Dashboard, Recommendations).
- Admin CSR uses `fetch` to `/api/products` for read/write.
- API routes call `lib/products` which use MongoDB if configured via `lib/db`, else fallback to JSON file at `data/products.json`.
- Create/Update operations set `lastUpdated` to ISO timestamps. Admin requests require `ADMIN_API_KEY`.

## Challenges & Solutions

- Mixed rendering strategies: Separated server and client boundaries with dedicated client components.
- Optional database: Implemented graceful fallback to JSON while supporting MongoDB via cached connection.
- No comments constraint: Used clear naming and file structure to preserve readability.

## Performance Considerations

- SSG for the home grid eliminates runtime work and maximizes CDN cache hits.
- ISR for product pages provides freshness without full rebuilds.
- SSR for dashboard ensures real-time accuracy at the cost of per-request compute.
- Client-side state only where necessary to avoid hydration overhead elsewhere.

## Screenshots

- Home Page: [screenshot]
- Product Detail: [screenshot]
- Dashboard: [screenshot]
- Admin Panel: [screenshot]
- Recommendations: [screenshot]
