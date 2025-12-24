# Homemade Soap Business Website (Full-Stack, Free Tier)

A full-stack website for a homemade soap business with:
- Product catalog
- Product details page
- Cart (localStorage)
- Checkout (creates order in DB)
- Admin panel (simple password-protected CRUD for products)
- SEO basics + performance optimizations
- Free deployment on Vercel + free database on MongoDB Atlas

> Goal: A real small-business ready MVP that can be built and deployed with ₹0 (using free tiers).

---

## Tech Stack

**Frontend + Backend (Full Stack in one repo)**
- Next.js (App Router) on Vercel

**Database**
- MongoDB Atlas (M0 free cluster)

**Email (optional)**
- EmailJS (send order/contact notifications)

---

## Features

### Customer Side
- Home page (brand story, highlights)
- Products listing with category filter
- Product detail page (price, description, images)
- Cart add/remove/update quantity (persistent)
- Checkout form:
  - Name, Phone, Address, Notes
  - Creates order and shows confirmation
  - WhatsApp deep-link after placing order (recommended for India)

### Admin Side
- Admin login (single password from env var)
- Add / edit / delete products
- Update stock and price

### Safety & Quality
- Input validation (basic)
- Rate limiting on APIs (recommended)
- Avoids committing secrets by using environment variables

---

## Project Structure (Recommended)

soap-store/
├─ app/
│  ├─ page.tsx                      # Home
│  ├─ products/
│  │  ├─ page.tsx                   # Catalog
│  │  └─ [id]/page.tsx              # Product detail
│  ├─ cart/page.tsx
│  ├─ checkout/page.tsx
│  ├─ admin/page.tsx
│  └─ api/
│     ├─ products/route.ts          # CRUD endpoints
│     └─ orders/route.ts            # Create orders
├─ components/
│  ├─ Navbar.tsx
│  ├─ ProductCard.tsx
│  ├─ CartItem.tsx
│  └─ Footer.tsx
├─ lib/
│  ├─ db.ts                         # Mongo connection (cached)
│  ├─ models.ts                     # Product + Order schemas
│  └─ validators.ts                 # simple validation helpers
├─ public/
├─ styles/
├─ .env.local.example
├─ .gitignore
└─ README.md

---

## Local Setup

### 1) Install
npm install

### 2) Create `.env.local`
Copy the example:
cp .env.local.example .env.local

Fill these values:
- `MONGODB_URI=...`
- `ADMIN_PASSWORD=...`

Optional:
- `EMAILJS_SERVICE_ID=...`
- `EMAILJS_TEMPLATE_ID=...`
- `EMAILJS_PUBLIC_KEY=...`

### 3) Run locally
npm run dev
Open:
- http://localhost:3000

---

## MongoDB Atlas Setup (Free)

1. Create an Atlas account and an M0 free cluster. [web:108]
2. Create DB user + password.
3. Network access:
   - For simplest MVP, allow access from anywhere (0.0.0.0/0) BUT this is less secure.
4. Copy the connection string and set `MONGODB_URI` in `.env.local`.

---

## Deployment (Free)

### Deploy to Vercel
1. Push this repo to GitHub
2. Go to Vercel → Import project → select this repo
3. Add Environment Variables in Vercel project settings:
   - `MONGODB_URI`
   - `ADMIN_PASSWORD`
4. Deploy

Vercel free plan details/limits are documented in Vercel’s Hobby plan docs. [web:103][web:111]

---

## Free Tier Limitations (Important)

### Vercel (Hobby plan)
- Has included usage limits (e.g., function invocations, CPU, bandwidth) and if you exceed some limits you may need to wait ~30 days to use the feature again. [web:103]
- Limits page includes project & deployment limits (example: 100 deployments/day on Hobby). [web:111]
- Function timeouts exist; maximum duration is configurable up to 60s on Hobby (depends on function settings). [web:103]
- Vercel Functions memory default/maximum on Hobby is 2 GB / 1 vCPU. [web:122]
**Practical impact:** keep APIs fast (don’t do heavy processing), compress images, and avoid large traffic spikes. [web:103][web:122]

### MongoDB Atlas (M0 Free cluster)
- M0 has documented configuration + operational limits; free clusters can auto-pause when idle. [web:108]
- M0 also has limits on number of databases/collections and certain unsupported commands/behaviors. [web:108]
**Practical impact:** keep data models simple, reuse a single cached DB connection, and don’t store huge image data in MongoDB. [web:108]

### EmailJS (Free)
- Free plan includes 200 monthly requests, 2 email templates, and request size up to 50 KB. [web:124]
**Practical impact:** for real businesses, WhatsApp confirmation or a server-side email provider is more reliable once orders grow. [web:124]

### Custom Domain
- A truly “professional” domain (like `.com` / `.in`) is typically paid yearly.
- You can use the free `*.vercel.app` URL initially and upgrade later.

---

## Recommended MVP Workflow (What to build first)

1. UI pages: Home → Products → Product detail → Cart → Checkout
2. DB: Product model + Order model
3. Admin: Add products + edit stock
4. Delivery flow: COD/UPI + WhatsApp confirmation message
5. SEO: page titles, meta descriptions, fast images

---

## Security Notes (MVP Level)
- Never commit `.env.local`
- Keep admin password strong
- Add rate-limiting to `/api/*` routes
- Validate all user input (phone, address length, item quantities)

---

## Roadmap (Next Up)
- Search + category filters
- Discount coupons
- Order status updates (confirmed/delivered)
- Payment integration (UPI/Stripe) after MVP
- Customer login (optional)
- Analytics dashboard

---

## License
MIT (optional)

---

## Author
- Name: <your name>
- GitHub: https://github.com/<your-username>

