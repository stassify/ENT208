# Campus Market — Technology Choices

<!-- WHAT IS A STACK?
A "stack" is the complete list of tools your app is built with — like a recipe listing
all the ingredients before you start cooking. Once you choose your stack, every feature
you build uses those same tools. Changing the stack mid-project is expensive. -->

---

## The big picture

Campus Market has two parts:


```
┌──────────────────────────┐        ┌──────────────────────────┐
│  FRONTEND                │  ───▶  │  BACKEND                 │
│  What the user sees      │        │  Where data is stored    │
│  Runs on the user's phone│  ◀───  │  Runs on a remote server │
│  Built with React        │        │  Supabase (PostgreSQL)   │
└──────────────────────────┘        └──────────────────────────┘
```


<!-- WHAT IS A FRONTEND?
The frontend is everything the user can see and tap.
It runs inside the browser on the user's phone.
It is built with three web languages:
  - HTML: the structure (headings, buttons, forms)
  - CSS: the look (colours, fonts, layout)
  - JavaScript: the behaviour (what happens when you tap a button) -->

<!-- WHAT IS A BACKEND?
The backend is the part the user never sees.
It stores data permanently (users, products, messages, orders).
It runs on a server — a computer that is always on and connected to the internet.
When the frontend needs data, it sends a request to the backend.
The backend sends the data back.
We do not build our own backend — we use Supabase, which runs it for us. -->

<!-- WHAT IS AN API?
An API (Application Programming Interface) is the way the frontend talks to the backend.
Think of it as a menu in a restaurant. The menu tells you what you can order.
You do not need to know how the kitchen works — you just pick from the menu.
Supabase generates an API automatically from our database tables. -->

---

## Frontend

### React + TypeScript — the framework

React is a JavaScript library for building user interfaces. It lets us build reusable components (ProductCard, SearchBar, etc.) and manage state efficiently. TypeScript adds type safety, catching errors early and making the code more maintainable for a team of students.

We chose React because:
- The team already knows it from coursework and tutorials
- It has a huge ecosystem and excellent documentation
- TypeScript prevents common bugs (e.g., passing wrong props to a component)

**Docs:** https://react.dev

### Vite — the build tool

<!-- WHAT IS A BUILD TOOL?
Your source code (TSX files, CSS, images) cannot be loaded directly by a browser.
A build tool "compiles" it — bundles all the files together and optimises them
so the browser can load the app quickly.
Vite also runs a local preview server so you can test on your laptop before deploying. -->

Vite is the standard build tool for modern React projects. It is extremely fast and requires almost no configuration. It supports hot module replacement (HMR), meaning changes appear instantly without a full page reload.

We chose Vite because:
- It is the default for new React projects (via `npm create vite@latest`)
- Fast startup and refresh speeds improve developer productivity
- Works seamlessly with TypeScript and Tailwind CSS

**Docs:** https://vitejs.dev

### Tailwind CSS — the styling framework

Tailwind is a utility‑first CSS framework. Instead of writing custom CSS, we compose styles using classes like `flex`, `p-4`, `bg-primary`, and `text-center`. This keeps the CSS bundle small and makes responsive design easy.

We chose Tailwind because:
- No context switching between CSS files and components
- Built‑in responsive modifiers (`sm:`, `md:`, `lg:`) make mobile‑first design simple
- The team has prior experience with Tailwind from other projects
- It integrates perfectly with shadcn/ui (see below)

**Docs:** https://tailwindcss.com

### shadcn/ui — the component library

shadcn/ui is not a traditional component library (no npm install of a giant package). Instead, it provides copy‑pasteable components built on Radix UI and styled with Tailwind. You own the code and can modify it as needed.

We use these shadcn components in the project:
- `Button`, `Card`, `Input`, `Textarea`, `Label`
- `Dialog`, `Tabs`, `Carousel`, `Avatar`, `Badge`
- `Checkbox`, `RadioGroup`, `Select`

We chose shadcn/ui because:
- It gives us professionally designed, accessible components for free
- No extra dependencies — we control every component's code
- Easy to customise colours to match our brand (using CSS variables)
- The components are built with Radix UI, which handles keyboard navigation and screen readers out of the box

**Docs:** https://ui.shadcn.com

### Lucide React — icons

We use Lucide React for icons (`Heart`, `ShoppingCart`, `MessageCircle`, `GraduationCap`, etc.). It provides a consistent set of SVG icons that are lightweight and customisable.

**Docs:** https://lucide.dev

---

## Backend

### Supabase — database, authentication, and API

<!-- WHAT IS A DATABASE?
A database stores data permanently and lets you search it quickly.
Think of it as a set of spreadsheets — each "table" is one spreadsheet.
Campus Market has tables for: users (profiles), products, orders, conversations, messages, reports, favourites. -->

Supabase is an open‑source Firebase alternative. It gives us:

| What | What it means |
|---|---|
| **PostgreSQL database** | A powerful relational database — users, products, orders, messages, etc. |
| **Auto‑generated REST API** | The frontend can read and write data without any server code |
| **Row‑Level Security (RLS)** | Rules that control who can see or change which rows (e.g., only the seller can edit their own product) |
| **Authentication** | Email/password login; we extend it with email domain whitelist (`@xjtlu.edu.cn`) |
| **Storage** | For product images (uploaded to Supabase Storage) |
| **Edge Functions** | Serverless functions (not heavily used in MVP, but available for future needs) |

We chose Supabase because:
- The API is generated automatically from our database tables — no server code to write or maintain for basic CRUD
- Row‑level security lets us enforce “only XJTLU students can access this” without building a complex auth system
- The free tier includes 500 MB database, 1 GB file storage, and 2 GB bandwidth — enough for hundreds of students
- It provides real‑time subscriptions (useful for chat messaging)
- The dashboard is a full database editor — the admin can view and edit data directly without touching code

**Docs:** https://supabase.com/docs

### Data model (simplified)

```
profiles (extends auth.users)
  id · student_id (masked) · role (buyer/seller/admin) · preferences_set · preferred_categories · etc.

products
  id · seller_id → profiles · title · description · category · price · images[] · is_active · is_sold · is_graduation · created_at

orders
  id · order_no · buyer_id → profiles · seller_id → profiles · product_id → products · status · created_at

conversations
  id · product_id → products · buyer_id → profiles · seller_id → profiles · updated_at

messages
  id · conversation_id → conversations · sender_id → profiles · content · created_at

reports
  id · product_id → products · reporter_id → profiles · reason · description · status · created_at

favourites
  id · user_id → profiles · product_id → products · created_at

meeting_requests
  id · product_id → products · buyer_id → profiles · seller_id → profiles · location_type · location_value · message · status · created_at
```


<!-- WHAT IS A DATA MODEL?
A data model is a diagram or list that shows what information you store and
how the pieces connect. An arrow (→) means "links to another table".
For example, a product row contains seller_id — this links it to the correct profile in the profiles table.
You do not store the seller's name in the product row — you store the seller's ID,
then look up the name when you need it. This avoids duplication. -->

---

## Hosting

### Vercel — frontend deployment

<!-- WHAT IS DEPLOYMENT?
Deployment means putting your finished app on a server so anyone with the link can open it.
Before deployment, only you can see the app running on your laptop.
After deployment, it is public (or password-protected) at a URL like campus-market.vercel.app. -->

Vercel hosts the frontend (the HTML, CSS, and JavaScript files the browser loads). It connects to our GitHub repository. Every time we push code to `main`, Vercel builds and deploys automatically. The URL updates within 30 seconds.

We chose Vercel because:
- Automatic deploys from GitHub — every push to `main` is live within 30 seconds
- Every pull request gets its own preview URL — useful for testing before merging
- Free tier with no credit card required
- Built‑in environment variable management (for Supabase keys)

**Docs:** https://vercel.com

### Supabase — hosted backend

Supabase is already a hosted service. We do not need to deploy or manage any backend servers. The free tier includes:
- 500 MB database
- 1 GB file storage
- 2 GB data transfer
- Up to 2 concurrent connections (more than enough for MVP usage)

---

## Summary

| Layer | Tool | Why |
|---|---|---|
| Frontend framework | React + TypeScript | Team knows it; type safety |
| Build tool | Vite | Fast, modern, zero config |
| Styling | Tailwind CSS | Utility‑first, responsive, no context switching |
| Component library | shadcn/ui | Accessible, customisable, copy‑paste |
| Icons | Lucide React | Consistent SVG set |
| Database + Auth + Storage | Supabase | Auto‑generated API, RLS, free tier, real‑time |
| Hosting | Vercel | Free, automatic deploys, preview URLs |
