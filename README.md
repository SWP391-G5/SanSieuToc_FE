# SanSieuToc — Frontend

> Sports Field Booking & Management Platform (SWP391)

The frontend client for **SanSieuToc**, a full-stack academic web application designed for sports field booking, facility operations, and multi-role sports community management.

Companion Backend Repository: [SanSieuToc_BE](https://github.com/SWP391-G5/SanSieuToc_BE)

---

## Overview

SanSieuToc connects sports enthusiasts with sports facility owners. The client application provides tailored interfaces for four user roles:
- **Customers**: Browse sports venues, inspect real-time slot availability, reserve fields and add-on services, participate in community discussions, and manage a personal digital wallet.
- **Field Owners**: Manage field information, operating schedules, booking orders, service requests, vouchers, and revenue analytics.
- **Managers**: Moderate community posts and customer reviews, manage promotional banner resources, monitor business performance across assigned facility owners, and maintain platform privacy policies.
- **Administrators**: Oversee platform accounts (managers, owners, customers), assign facility owners to managers, and review system reports.

---

## Key Features

- **Venue Discovery & Booking**: Interactive field catalog with filtering, time-slot selection, service add-ons, and booking checkout.
- **Role-Based Workspaces**: Dedicated layouts, navigation trees, and route guards for Customer, Owner, Manager, and Administrator workspaces.
- **Analytics Visualization**: Interactive revenue and booking trend charts powered by Recharts.
- **Community Moderation**: Content publishing, Cloudinary image upload workflows, and review moderation.
- **Digital Wallet**: Balance tracking, top-up workflow, and transaction ledger.

---

## Technology Stack

The client is built with the following libraries and tools (versions declared in `package.json`):

- **Core Framework & Build Tool**: React (`^19.2.3`), Vite (`^7.2.4`)
- **Routing**: React Router DOM (`^7.12.0`)
- **Styling & Icons**: TailwindCSS (`^3.4.19`), PostCSS (`^8.5.6`), Autoprefixer (`^10.4.23`), Lucide React (`^0.562.0`), React Icons (`^5.5.0`)
- **Data Fetching & State**: Axios (`^1.13.2`), TanStack React Query (`^5.99.2`), Redux Toolkit (`^2.11.2`)
- **Data Visualization**: Recharts (`^3.8.1`)
- **Forms & Tables**: React Hook Form (`^7.71.1`), Headless UI (`^2.2.9`), TanStack React Table (`^8.21.3`)
- **UI Utilities**: Swiper (`^12.0.3`), React Modal (`^3.16.3`), Leaflet / React-Leaflet (`^5.0.0`), QR Code (`^4.2.0`), i18next (`^25.8.14`)

---

## Application Structure

```text
src/
├── assets/          # Static media and brand assets
├── components/      # Shared UI elements and role-based route guards
│   ├── common/      # General shared UI components
│   ├── manager/     # Manager route guard (RequireManager)
│   └── owner/       # Owner route guard (RequireOwner)
├── config/          # Central API endpoints catalog (api.config.js)
├── context/         # AuthContext, NotificationContext, ThemeContext, PreviewModeContext
├── layouts/         # Layout shells (MainLayout, ManagerLayout, OwnerLayout, AdminLayout)
├── pages/           # Screen modules grouped by user role
│   ├── Customer/    # Field listings, booking, community, reviews, policy
│   ├── Manager/     # Analytics, post moderation, banners, feedback, wallet
│   ├── owner/       # Field management, bookings, refunds, revenue, vouchers
│   ├── admin/       # Account administration and system reports
│   ├── auth/        # Authentication, registration, password recovery
│   └── Payment/     # Checkout and wallet top-up
├── services/        # Axios HTTP client instance and domain API connectors
└── utils/           # Formatters, date helpers, and validation utilities
```

---

## User Roles

1. **Customer**: Public exploration, venue booking, service reservations, community interaction, and wallet top-ups.
2. **Owner**: Operational management of sports facilities, field slots, customer reservations, and revenue.
3. **Manager**: Platform content moderation, scoped business intelligence, banner placements, and legal terms maintenance.
4. **Administrator**: User account provisioning, role assignment, and platform-wide monitoring.

---

## Team Contributions

This application was developed as a collaborative academic project for the **SWP391** course by a team of five students. Work was partitioned across primary functional workflows:

- **Phạm Quốc Minh (MinhPQ)**: Fullstack Developer — Manager Module (Revenue Analytics, Post Moderation, Banner Placements, Customer Review Moderation & Notices, Privacy Policies, Wallet & Withdrawals)
- **Nguyễn Việt Đức (DucNV)**: Fullstack Developer — Owner Module (Field Operations, Add-on Services, Bookings & Slots, Vouchers, Owner Revenue Analytics)
- **Nguyễn Viết Sang (SangNV)**: Fullstack Developer — Admin & Authentication Flow (Role-Based Access Control, Manager & Owner Account Provisioning, Customer Account Moderation, Authentication & User Profiles)
- **Nguyễn Thành An (AnNVT)**: Fullstack Developer — Customer Booking & Payments Module (Wallet Management, Top-Up, Checkout, Add-on Services, Transactions & Refunds)
- **Hoàng Thành Long (LongHT)**: Fullstack Developer — Customer Experience & Community Module (Home Page, Field Discovery & Filtering, Wishlist, Community Posts, Reviews & Feedback)

*Note: Work assignments reflect course planning and module ownership across the team.*

---

## Manager Module — Technical Overview

**Primary Contributor**: Phạm Quốc Minh  
**Role**: Fullstack Developer — Manager Module

The Manager actor serves as an operational supervisor between system administrators and field owners. The module implementation spans both the React frontend and Express/MongoDB backend:

### Key Implemented Capabilities

1. **Scoped Business Intelligence & Analytics (`ManagerStatisticsPage.jsx`)**:
   - Aggregates KPIs across orders, reserved court slots, gross revenue, refunds, and net revenue.
   - Interactive trend visualization with Recharts (Line and Bar charts) supporting daily, weekly, and monthly time-grain groupings.
   - Presets for rapid filtering (Today, Last 7 Days, This Month, This Year).
   - Scoped Owner Selector: filters analytics to only the facility owners specifically assigned to the active manager.
   - "Hot Fields" ranking displaying top-utilized courts with detail preview modals.

2. **Community & Post Moderation (`ManagerPostsPage.jsx`)**:
   - Review workflows (Approve, Reject, Delete) for posts submitted by community members and field owners.
   - Scoped moderation: verifies that an owner post belongs to an owner within the manager's assigned scope before approving.
   - Manager announcement creation supporting up to 6 image uploads via Cloudinary and topical tags.
   - Database-backed draft persistence via API (`status: 'Draft'`). Deprecated client-only draft storage shims are retained for backward compatibility.

3. **Banner & Marketing Placements (`BannersAdsPage.jsx`)**:
   - Management interface for promotional banners and sliders (`MarketingResource`).
   - Placement selection, active status toggle, and duplicate sequence order validation.

4. **Customer Feedback Moderation (`ManagerFeedbackPage.jsx`)**:
   - Moderation table showing customer reviews across fields in the manager's assigned scope.
   - Soft-deletion requiring a documented violation reason, triggering an automated email notification to the reviewer.
   - Audit view of removed reviews with restoration support.

5. **Platform Privacy Policies (`ManagerPrivacyPage.jsx`)**:
   - Accordion-style CRUD interface for system privacy and policy documents.

6. **Manager Wallet & Withdrawals (`ManagerWalletPage.jsx`, `ManagerWithdrawPage.jsx`)**:
   - Digital balance viewing, transaction history ledger, and bank withdrawal requests with account format validation.

---

## Getting Started

### Prerequisites
- **Node.js**: Compatible with Vite 7 engines (`^18.0.0 || ^20.0.0 || >=22.0.0`). Node.js LTS (20.x or 22.x) is recommended.
- **npm** (v9+) or **yarn**

### Installation & Local Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/SWP391-G5/SanSieuToc_FE.git
   cd SanSieuToc_FE
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Configure environment:
   Create a `.env` file based on `.env.example`:
   ```bash
   cp .env.example .env
   ```
   Default configuration:
   ```env
   # Backend API Base URL
   VITE_API_URL=http://localhost:9999

   # Local Development UI Preview Flag (optional)
   VITE_BYPASS_MANAGER_AUTH=false
   ```

4. Launch development server:
   ```bash
   npm run dev
   ```
   The client will be accessible at `http://localhost:5173`.

5. Build for production:
   ```bash
   npm run build
   ```

---

## Development Configuration

### API Routing & Proxy
- **Axios HTTP Client**: Requests configured through `src/services/axios.js` use `import.meta.env.VITE_API_URL` (defaulting to local `http://localhost:9999`).
- **Development Server Proxy**: In `vite.config.js`, the Vite dev server forwards `/api` requests to `VITE_API_URL` or `http://localhost:9999`. This ensures components using relative `fetch('/api/...')` routes seamlessly reach the local backend.

### Manager UI Preview Mode
- Setting `VITE_BYPASS_MANAGER_AUTH=true` allows developers to bypass the client-side `RequireManager` route guard during UI layout work.
- **Important Limitations**:
  - The bypass is strictly gated to local development (`import.meta.env.DEV`) and is automatically inactive in production builds.
  - It bypasses only the frontend route guard; it does **not** create a backend session or bypass backend JWT verification.
  - Endpoints requiring authentication will return `401 Unauthorized` without a running backend and valid user session.

---

## Backend Integration

The client application integrates with the companion backend service:
- Bearer tokens are stored in `localStorage` (`sst_auth`) and attached via Axios request interceptors.
- Centralized endpoint constants are cataloged in `src/config/api.config.js`.

---

## Academic Documentation Notice

Course-level specifications (Software Design Specification — SDS, Requirements Document — RDS, and Draw.io system diagrams) were authored during the SWP391 semester and are retained in private project archives. They are not bundled inside this public client repository.

---

## Related Repository

- **Backend Repository**: [https://github.com/SWP391-G5/SanSieuToc_BE](https://github.com/SWP391-G5/SanSieuToc_BE)