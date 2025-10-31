# Next.js E-Commerce

A Next.js e-commerce app demonstrating SSG, ISR, SSR, and CSR with a products API and JSON/MongoDB data.

## Setup

1. Install dependencies
```bash
npm install
```
2. Create environment file
- Copy `env.example` to `.env.local`
- Set `MONGODB_URI` (optional)
- Set `ADMIN_API_KEY`

## Run
```bash
npm run dev
```

## Rendering Strategies

- Home (`/`, `app/page.tsx`): SSG with `revalidate = false` and client search/filter.
- Product Detail (`/products/[slug]`): ISR with `revalidate = 60`, `generateStaticParams`.
- Dashboard (`/dashboard`): SSR with `dynamic = 'force-dynamic'` and live stats.
- Admin (`/admin`): CSR with client fetch and forms.
- Recommendations (`/recommendations`): Server list with client wishlist.

## API Endpoints

- GET `/api/products`
- POST `/api/products` (requires `ADMIN_API_KEY` header)
- GET `/api/products/[slug]`
- PUT `/api/products/[id]` (requires `ADMIN_API_KEY` header)

Payload
```
name, slug, description, price, category, inventory
```

## Database Schema
```
{
  id: string,
  name: string,
  slug: string,
  description: string,
  price: number,
  category: string,
  inventory: number,
  lastUpdated: string
}
```

## Features

- Tailwind styling and responsive grids
- Validation and loading states
- Optional MongoDB, JSON fallback

## Notes

If MongoDB is not configured, data persists to `data/products.json`.
