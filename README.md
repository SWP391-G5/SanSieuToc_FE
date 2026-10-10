# SanSieuToc — Frontend

> Sports Field Booking & Management Platform (SWP391 — FFMS)

The frontend client for **SanSieuToc** (Football/Sports Field Management System — FFMS), an academic full-stack web application designed for sports field booking, facility operations, and multi-role sports community management.

Companion Backend Repository: [SanSieuToc_BE](https://github.com/SWP391-G5/SanSieuToc_BE)

---

## Overview

SanSieuToc connects sports enthusiasts with field owners. The frontend provides specialized experiences for four distinct actors:
- **Customers**: Browse venues, check slot availability, book fields, hire additional services, join community discussions, and top up personal wallets.
- **Field Owners**: Manage field schedules, track bookings and service orders, analyze revenue, and process refunds.
- **Managers**: Moderate platform posts and reviews, configure promotional banners, monitor business metrics across assigned owners, and maintain platform policies.
- **Administrators**: Oversee user accounts, assign managers to owners, and view high-level platform audit reports.

---

## Key Features

- **Dynamic Booking & Availability**: Real-time slot selection, service add-ons, and integrated checkout.
- **Role-Based Workspaces**: Dedicated layouts and navigation for Customer, Owner, Manager, and Admin actors.
- **Interactive Analytics**: Revenue and booking trend visualization powered by Recharts.
- **Community & Content Management**: Post creation, image uploads via Cloudinary, and status-based moderation workflows.
- **Wallet & Transactions**: Top-up flow, balance display, and transaction ledger.

---

## Technology Stack

- **Core & Build Tooling**: React 19 (`19.2.3`), Vite 7 (`7.2.4`)
- **Routing**: React Router DOM 7 (`7.12.0`)
- **Styling**: TailwindCSS 4 (`4.1.18`), Lucide React, React Icons
- **Data Management & API**: Axios (`1.13.2`) with request interceptors, TanStack React Query
- **Data Visualization**: Recharts (`3.6.0`)
- **Forms & Components**: React Hook Form, Headless UI, TanStack React Table, Swiper

---

## Application Structure

```text
src/
├── assets/          # Static media and brand assets
├── components/      # Shared UI elements and route guards
│   ├── common/      # General UI components
│   ├── manager/     # Manager guard (RequireManager)
│   └── owner/       # Owner guard (RequireOwner)
├── config/          # Central API endpoints configuration (api.config.js)
├── context/         # AuthContext, NotificationContext, ThemeContext
├── layouts/         # Layout shells (MainLayout, ManagerLayout, OwnerLayout, AdminLayout)
├── pages/           # Screen modules grouped by user role
│   ├── Customer/    # Field listings, booking, community, policy
│   ├── Manager/     # Analytics, post moderation, banners, feedback, wallet
│   ├── owner/       # Field management, bookings, refunds, revenue
│   ├── admin/       # Account administration and system reports
│   ├── auth/        # Login, registration, password recovery
│   └── Payment/     # Checkout and wallet top-up
├── services/        # Axios client instance and domain API connectors
└── utils/           # Formatters, date helpers, and validation utilities
```

---

## User Roles

1. **Customer**: Public exploration, field reservations, community engagement, reviews, and wallet top-ups.
2. **Owner**: Operations hub for sports facility owners to oversee bookings, field slots, and revenues.
3. **Manager**: Content moderation, scoped business intelligence, banner scheduling, and policy enforcement.
4. **Admin**: Platform-level user management and account authorization.

---

## My Contribution — Manager Module

**Developer**: Phạm Quốc Minh (MinhPQ)  
**Role**: Fullstack Developer — Manager Module

I was responsible for the end-to-end full-stack implementation of the **Manager** actor workspace:

### Implemented Capabilities

1. **Business Intelligence & Analytics (`ManagerStatisticsPage.jsx`)**:
   - Orchestrated KPI cards displaying total orders, slots reserved, gross revenue, refund deductions, and net revenue.
   - Built interactive Line and Bar charts using **Recharts** with day/week/month aggregation and time-range presets (Today, Last 7 Days, This Month, This Year).
   - Implemented an **Owner Scoping Selector**, allowing managers to filter analytics across their specifically assigned facility owners.
   - Designed a "Hot Fields" ranking view and field detail inspection modal.

2. **Community & Post Moderation (`ManagerPostsPage.jsx`)**:
   - Developed moderation workflows (Approve, Reject, Delete) for posts submitted by community members and field owners.
   - Implemented manager-authored post creation with multi-image Cloudinary uploads (up to 6 images) and tagging.
   - Built a local storage and database draft persistence mechanism (`status: 'Draft'`).

3. **Banner & Marketing Placements (`BannersAdsPage.jsx`)**:
   - Built the management interface for homepage hero banners and sliders (`MarketingResource`).
   - Implemented placement selection, active toggle controls, and duplicate order sequence validation.

4. **Customer Feedback Moderation (`ManagerFeedbackPage.jsx`)**:
   - Designed an aggregated feedback monitoring table across all fields in the manager's scope.
   - Implemented a reason-based soft-deletion workflow, triggering an automated email notification to the reviewer.
   - Provided audit inspection of deleted reviews with instant restoration capabilities.

5. **Platform Privacy Policies (`ManagerPrivacyPage.jsx`)**:
   - Developed an accordion-based CRUD management interface for public legal and privacy terms.

6. **Manager Wallet & Payouts (`ManagerWalletPage.jsx`, `ManagerWithdrawPage.jsx`)**:
   - Implemented balance tracking, transaction history tables, and bank withdrawal requests with strict account format validation.

---

## Getting Started

### Prerequisites
- Node.js (v18 or higher recommended)
- npm or yarn

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

3. Create environment configuration file:
   Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```
   Or create `.env` manually:
   ```env
   VITE_API_URL=http://localhost:9999

   # Quick UI Evaluation / Preview Mode:
   # Set to true to bypass manager route guard during local layout development
   VITE_BYPASS_MANAGER_AUTH=true
   ```

   > **Note on Evaluation / Offline DB**: Since cloud database instances from the academic semester are now offline, set `VITE_BYPASS_MANAGER_AUTH=true` to navigate and evaluate the Manager UI screens (`/manager/statistics`, `/manager/posts`, etc.) without requiring an active backend or authentication session.

4. Launch development server:
   ```bash
   npm run dev
   ```
   The application will start at `http://localhost:5173`.

5. Build for production:
   ```bash
   npm run build
   ```

---

## Backend Integration

The frontend communicates with the backend via a centralized Axios instance (`src/services/axios.js`) configured with:
- Bearer token authentication automatically attached from `localStorage` (`sst_auth`).
- Central endpoint catalog defined in `src/config/api.config.js`.
- Error normalization for structured server responses.

---

## Team Contributions

This project was developed for the **SWP391** academic course by **Group 5 (5 members)**. The official responsibilities as documented in the course scope matrix (`Docs/Scope.xlsx` & `ProjectTracking`):

- **Phạm Quốc Minh (MinhPQ)**: Fullstack Developer — Manager Module (Revenue Analytics, Post Moderation, Banner/Ads, Customer Feedback Moderation & Notice, Privacy Policy, Wallet & Withdrawals)
- **Nguyễn Việt Đức (DucNV)**: Fullstack Developer — Owner Module (Field Operations, Field Services, Bookings & Slots, Vouchers, Owner Revenue Analytics)
- **Nguyễn Viết Sang (SangNV)**: Fullstack Developer — Admin & Authentication Flow (System RBAC, Manager & Owner Account Provisioning, Customer Account Moderation, Auth & Security, User Profiles)
- **Nguyễn Thành An (AnNVT)**: Fullstack Developer — Customer Booking & Payment Module (Wallet Operations & Top-Up, Checkout & Booking Confirmation, Service Add-ons, Transactions & Refunds)
- **Hoàng Thành Long (LongHT)**: Fullstack Developer — Customer Experience & Community Module (Home Page, Field Discovery & Filtering, Wishlist, Community Posts, Reviews & Feedback)

---

## Academic Project Documentation

Original academic project specifications, architecture documents, and diagrams are stored in the project repository's `Docs/` directory:
- **Software Design Specification (SDS)**: `Docs/SWP391_G5-FFMS_SDS Document.docx`
- **Requirements Specification (RDS)**: `Docs/SWP391_G5-FFMS_RDS Document.docx`
- **Architecture & System Diagrams**: `Docs/Diagrams` (Draw.io format: ERD, use cases, sequence diagrams)
- **Project Scope Matrix**: `Docs/Scope.xlsx` & `Docs/SWP391_G5-FFMS_ProjectTracking_v1.0.xlsx`

---

## Related Repository

- **Backend Repository**: [https://github.com/SWP391-G5/SanSieuToc_BE](https://github.com/SWP391-G5/SanSieuToc_BE)