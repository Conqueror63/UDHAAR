Deployment LINK : https://smart-asset-management-and-resource-sigma.vercel.app/

# AssetFlow – Smart Asset Management & Resource Allocation Platform

## Overview
AssetFlow is a full-stack web application built for the Cultural Council of IIT Roorkee. It offers a centralized dashboard to track, manage, reserve, and maintain assets like cameras, microphones, stage lights, props, costumes, and event equipment. Admins can manage inventory, approve/reject booking requests, handle QR-based checkouts and returns, and audit system activity. Regular members can browse assets, check availability, and submit booking requests.

## Tech Stack
- **Framework:** Next.js 15 (App Router) + TypeScript
- **Styling:** Tailwind CSS v4 with PostCSS
- **Database:** PostgreSQL via Prisma ORM
- **Auth:** NextAuth.js (Credentials + Google/GitHub OAuth)
- **Other tools:** Recharts (analytics), html5-qrcode (scanning), qrcode (label generation), Cloudinary (avatar hosting)

## Architecture
A unified Next.js App Router stack where Server Actions talk directly to the database via Prisma, with route protection handled by NextAuth middleware.

```
User → Next.js App → NextAuth → Prisma ORM → PostgreSQL
```

## Features

### Authentication & Onboarding

### Asset Browsing & Booking

### Checkout & Return Workflow

### Admin Console

### Audit Logging

---
### Run Locally
```bash
npm run dev
```
Visit `http://localhost:3000`.

### Production Build
```bash
npm run build
npm run start
```

## Test Accounts
**Admin**
- Email: `admin@cultural.iitr.ac.in`
- Password: `AdminPassword123`

**Member**
- Email: `rohan@cultural.iitr.ac.in`
- Password: `MemberPassword123`

## Project Structure
```
src/
├── app/
│   ├── actions/      # Server Actions
│   ├── admin/        # Admin dashboards
│   ├── api/          # Auth endpoints
│   ├── dashboard/    # Member dashboards
│   └── login/        # Sign-in page
├── components/       # Shared UI (Header, Sidebar, forms)
├── lib/              # DB connection, auth config
├── hooks/            # Custom hooks
└── types/            # Auth type defs

prisma/
├── schema.prisma     # DB schema
└── seed.js           # Seed script

docs/                 # Architecture docs & screenshots
```

## Server Actions
Instead of public API routes, the app uses server actions grouped as:
- **auth** – registration handling
- **profile** – name/section updates, avatar uploads (Cloudinary)
- **assets** – CRUD + checkout overlap logic
- **bookings** – requests, approvals, cancellations
- **operations** – checkout/check-in flows with QR verification
- **users** – permission/role management
- **audit** – secure audit log access

## Database Models
- **User** – credentials, OAuth links, club section, role
- **Account / Session** – NextAuth tables
- **Asset** – descriptions, categories, quantities, QR data
- **Booking** – reservations, quantities, status, return confirmation
- **ReturnLog** – return condition and admin notes
- **MaintenanceLog** – repair/damage tracking
- **AuditLog** – immutable admin action records (JSON)
- **Notification** – user status alerts
