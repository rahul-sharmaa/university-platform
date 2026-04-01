# UniRank India — University Discovery Platform

A modern, SEO-friendly university discovery and lead-generation platform for India. Built with Next.js 15, PostgreSQL, Prisma, and Tailwind CSS.

## Features

- **Public site**: Homepage, university listing with filters, SEO-optimized detail pages, lead capture forms
- **Admin panel**: Dashboard, university CRUD, lead management, revision approval workflow, audit logging
- **SEO**: SSR/ISR, JSON-LD schema markup, breadcrumbs, clean URLs, meta tags, sitemap-ready
- **Role-based access**: Super Admin and University Admin with permission matrix
- **Lead generation**: "Apply Now" forms with validation, rate limiting, and routing

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 15 (App Router) |
| Language | TypeScript |
| Database | PostgreSQL |
| ORM | Prisma |
| Styling | Tailwind CSS |
| Auth | NextAuth.js v5 |
| Validation | Zod |
| Icons | Lucide React |
| Hosting | Vercel + Neon |

## Getting Started

### Prerequisites

- Node.js 20+
- PostgreSQL 15+ (local or hosted)
- npm

### 1. Clone and install

```bash
git clone https://github.com/your-org/university-platform.git
cd university-platform
npm install
```

### 2. Set up environment

```bash
cp .env.example .env
```

Edit `.env` with your database URL and secrets:

```
DATABASE_URL="postgresql://user:password@localhost:5432/university_platform"
NEXTAUTH_SECRET="generate-with-openssl-rand-base64-32"
NEXTAUTH_URL="http://localhost:3000"
```

### 3. Set up database

```bash
# Push schema to database
npx prisma db push

# Seed with sample data (5 IITs + admin user)
npm run db:seed
```

### 4. Run development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) for the public site.
Open [http://localhost:3000/admin](http://localhost:3000/admin) for the admin panel.

### Default admin credentials

- Email: `admin@unirank.in`
- Password: `admin123`

## Deploying to Vercel + Neon

### 1. Create a Neon database

1. Sign up at [neon.tech](https://neon.tech)
2. Create a new project
3. Copy the connection string

### 2. Deploy to Vercel

1. Push your code to GitHub
2. Import the repository in [Vercel](https://vercel.com/new)
3. Add environment variables:
   - `DATABASE_URL` — your Neon connection string
   - `NEXTAUTH_SECRET` — generate with `openssl rand -base64 32`
   - `NEXTAUTH_URL` — your production URL (e.g., `https://unirank.in`)
   - `REVALIDATION_SECRET` — any random string for ISR
4. Deploy

### 3. Run migrations and seed

```bash
# After first deploy, run in Vercel CLI or locally with production DATABASE_URL
npx prisma db push
npm run db:seed
```

## Project Structure

```
src/
├── app/
│   ├── (public)/          # Public pages (homepage, listing, detail)
│   ├── (admin)/admin/     # Admin panel pages
│   ├── api/               # API routes
│   └── auth/              # Auth pages
├── components/
│   ├── ui/                # Base UI components
│   ├── university/        # University card, detail components
│   ├── filters/           # Filter sidebar
│   ├── forms/             # Lead form
│   ├── admin/             # Admin layout, tables
│   └── layout/            # Header, footer, breadcrumbs
├── lib/
│   ├── auth/              # NextAuth config, permissions
│   ├── db/                # Prisma client
│   ├── validation/        # Zod schemas
│   └── utils/             # Helpers, audit logging
├── types/                 # TypeScript types
└── middleware.ts           # Auth middleware
```

## API Endpoints

### Public

| Method | Path | Description |
|---|---|---|
| GET | `/api/universities` | List with filters and pagination |
| GET | `/api/universities/:slug` | University detail |
| GET | `/api/search?q=...` | Search autocomplete |
| GET | `/api/filters` | Filter options with counts |
| POST | `/api/leads` | Submit lead form |

### Admin (auth required)

| Method | Path | Description |
|---|---|---|
| GET | `/api/admin/dashboard` | Dashboard stats |
| GET/POST | `/api/admin/universities` | List/create universities |
| GET/PUT/DELETE | `/api/admin/universities/:id` | CRUD university |
| GET | `/api/admin/leads` | List leads |
| PUT | `/api/admin/leads/:id` | Update lead status |
| GET | `/api/admin/revisions` | List pending revisions |
| PUT | `/api/admin/revisions/:id` | Approve/reject revision |

## Scripts

```bash
npm run dev          # Start dev server
npm run build        # Production build
npm run start        # Start production server
npm run lint         # Run ESLint
npm run type-check   # TypeScript check
npm run db:push      # Push schema to DB
npm run db:seed      # Seed sample data
npm run db:studio    # Open Prisma Studio
```

## License

MIT
