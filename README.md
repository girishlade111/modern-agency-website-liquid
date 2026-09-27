# Modern Agency Website — Liquid

A modern digital-agency marketing website with a "liquid" glassmorphism design: animated WebGL plasma/lightning hero effects, service features, logo marquee, pricing, checkout, FAQ, terms & conditions, and an admin dashboard. Originally generated with [v0.app](https://v0.app) and maintained as a full Next.js project.

## Features

- **Animated liquid hero** — WebGL-based `plasma.tsx` / `lightning.tsx` canvas effects (built with `ogl`)
- **Marketing pages** — About, Pricing, FAQ, Revisions, Terms & Conditions (`app/About`, `app/faq`, `app/t&c`, …)
- **Checkout + order form** — `app/checkout/page.tsx` and `components/order-form.tsx`
- **Admin panel** — `app/admin` with login page (`app/admin/login`)
- **Geo-aware pricing** — `app/api/geo` detects the visitor's country and returns INR vs USD pricing currency
- **Logo marquee + YouTube grid** — social-proof sections with lazy-loaded video components
- **SEO basics** — dynamic `robots.txt` and `sitemap.xml` route handlers
- **Dark theme support** — via `next-themes`, Radix UI primitives, Tailwind CSS v4, Geist font
- **Analytics ready** — `@vercel/analytics` integrated

## Tech stack

| Layer     | Tech                                                        |
|-----------|-------------------------------------------------------------|
| Framework | Next.js 15.2 (App Router), React 19, TypeScript              |
| Styling   | Tailwind CSS v4, tailwindcss-animate, Geist                   |
| UI kit    | Radix UI primitives, shadcn/ui-style `components/ui`          |
| Effects   | `ogl` (WebGL plasma/lightning), framer-motion-ready CSS      |
| Forms     | react-hook-form, zod, @hookform/resolvers                    |
| Charts    | recharts                                                     |
| Deploy    | Vercel (original target), also deployable anywhere Next.js runs |

## Quick start

```bash
# install (pnpm or npm)
pnpm install        # or: npm install --legacy-peer-deps

# run the dev server
pnpm dev            # or: npm run dev

# production build
pnpm build && pnpm start
```

Open http://localhost:3000 to view the site.

> **Security note:** if you keep `next` at `15.2.4`, bump it to `15.2.8` or newer (`npm i next@15.2.8`) — earlier 15.2.x releases are affected by CVE-2025-55182 (React2Shell RCE).

## Project structure

```
app/                    # App Router pages & routes
  page.tsx              # landing page (hero, features, marquee, pricing, footer)
  About/ faq/ t&c/      # marketing/info pages
  checkout/             # checkout page
  admin/                # admin panel + login
  api/geo/route.ts      # country→currency API
  robots.txt/ sitemap.xml/  # SEO route handlers
components/             # site sections (hero, pricing, footer, order-form, …)
  ui/                   # Radix-based primitives
  plasma.tsx lightning.tsx  # WebGL liquid effects
lib/                    # utilities
public/                 # images, icons
styles/                 # global styles
files                   # v0 design-export notes (reference only)
```

## Environment variables

No required env vars for the core site. `@vercel/analytics` works out of the box on Vercel. If you add your own backends (checkout/orders), put their secrets in `.env.local` (never commit them — `.env*` is already gitignored).

## Deployment notes

- The original deployment target was **Vercel** (v0 sync). Any platform that runs Next.js works (Vercel, Netlify, a Node host).
- `next.config.mjs` sets `images.unoptimized: true`, so no image-optimization backend is needed.
- **Static export caveat:** this app uses a server route (`app/api/geo`) and dynamic SEO routes, so `output: 'export'` static export is not supported as-is — deploy to a Node-capable host if you keep those routes. If you only need the marketing pages, you can remove `app/api/geo` and the admin/checkout pages and then export statically.

---

Built by Girish Lade — https://ladestack.in
