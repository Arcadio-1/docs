# Clarification Request: Outstanding Feature Specifications

**From:** Development Team
**To:** Business, Product & Design Teams
**Date:** June 9, 2026
**Subject:** Specification and design gaps blocking implementation of remaining modules

---

We've reached a point where several modules need detailed specifications and UI/UX designs before development can continue. Below are the areas where we need product decisions, design documentation, and wireframes/mockups from the design team. Each section includes what we've already built for context.

> **Note for the Design Team:** Each section contains a "Design deliverables needed" callout listing the screens, flows, and components we need designed. These are blocking frontend implementation — we cannot build what hasn't been designed.

---

## 1. Super Admin Panel — Company & User Management

**What exists today:** The super admin panel currently has a functional dashboard (system statistics), notification center (tickets, company approvals, edit approvals), roles & permissions management, and admin profile management. However, the **Company Management page is a placeholder** with no functionality implemented yet.

**What we need clarified:**

- What is the full scope of company oversight from the super panel? Specifically:
  - Should super admins be able to **view and edit** company profiles, or only view them?
  - Should super admins be able to **manage users within a company** (view user lists, edit user details, deactivate users), or is that exclusively within each company's own panel?
  - What company-level actions should be available? (e.g., suspend company, approve registration, change subscription tier)
  - Should there be an **activity log** showing changes made by super admins to company data?
- How does the company approval workflow interact with company self-registration? (We currently have company registration and edit-approval flows in the notification center — should company management consolidate these?)

**Design deliverables needed:**
- Company management list view (search, filter, status indicators)
- Company detail/overview screen from super admin perspective
- Company edit form (if editing is in scope)
- User list within a company (if user management from super panel is in scope)
- Company status change flow (suspend, reactivate, etc.)

---

## 2. Payment System & Transaction Management

**What exists today:** The wallet module has a complete **account statement** feature (transaction history, invoices, subscriptions, bookings with detail modals), a credit balance display, promotional offer cards, and credit package cards. The **payment form UI is built** (order summary, success modal), but **Stripe integration is not implemented** — it currently simulates payment locally.

**What we need clarified:**

- **Stripe integration scope:**
  - Which Stripe payment methods should be supported? (Cards only, or also SEPA direct debit, bank transfers, etc.?)
  - Should we implement Stripe Checkout (redirect to Stripe-hosted page) or Stripe Elements (embedded form in our UI)?
  - How should failed/declined payments be handled from the user's perspective?

- **Credit system:**
  - How do purchased credits and promotional/earned credits interact? Are they drawn from the same balance or tracked separately?
  - Is there a credit expiration policy?
  - Can credits be transferred between companies?

- **Withdrawal requests:**
  - Is there a scenario where companies need to **withdraw funds** (e.g., refunds, earned revenue from shared displays)?
  - If yes, what is the approval flow? (Company requests → super admin reviews → payout processed?)
  - What withdrawal methods should be supported?

- **Manual adjustments:**
  - Should super admins have the ability to **manually add or deduct credits** from a company's balance? (e.g., for compensation, corrections, promotional grants)
  - If yes, should these manual adjustments be logged and visible in the account statement?

- **Super admin payment oversight:**
  - The **Tariff Management page in the super panel is currently a placeholder.** What should it include? (Create/edit subscription tiers, set pricing, assign tariffs to companies?)
  - Should super admins have a global view of all transactions across companies?

**Design deliverables needed:**
- Payment checkout flow (Stripe Checkout redirect vs. embedded Stripe Elements — depends on product decision)
- Payment failure/retry screens
- Withdrawal request form and status tracker (company side, if withdrawals are in scope)
- Withdrawal review/approval queue (super admin side)
- Manual credit adjustment form (super admin side)
- Tariff management CRUD screens (super admin side — list, create, edit, assign)
- Global transaction overview dashboard (super admin side)

---

## 3. Schedule Feature — Admin Oversight

**What exists today:** Companies can create time-based schedules, assign playlists to time slots, and deploy them to displays. This is fully functional within the company panel.

**What we need clarified:**

- Should super admins be able to **view schedules** across all companies? (e.g., for auditing what content is deployed on which displays)
- Should super admins be able to **modify or override** a company's schedule? (e.g., force-remove content, insert emergency announcements)
- Are there any scheduling conflict rules that need enforcement at the platform level?

**Design deliverables needed:**
- Super admin schedule overview screen (cross-company view — if in scope)
- Schedule override/intervention UI (if modification rights are granted)

---

## 4. Content Reporting System

**What exists today:** The notification center (both company and super panel) already handles **support tickets, messages, notifications, company approvals, and edit approvals**. There is no dedicated content report/moderation module.

**What we need clarified:**

- Should content reports (e.g., inappropriate media, policy violations) be handled as a **separate module** with its own queue, statuses, and workflows?
- Or should content reports be managed **within the existing ticket/notification system** as a specific ticket category?
- What actions should be available on reported content? (e.g., remove content, warn company, suspend display, escalate to a different team)
- Who can submit content reports — only super admins, or also partner companies viewing shared displays?

**Design deliverables needed:**
- If separate module: report queue list view, report detail screen, moderation action panel
- If integrated into tickets: updated ticket creation form with "content report" category, reported content preview within ticket detail
- Content report submission flow (for whoever is allowed to submit)

---

## 5. Offer Module — Packages, Subscriptions & Targeted Offers

**What exists today:** The wallet module displays **promotional offers** and **credit packages** on the company side. The super panel has a placeholder tariff management page but no offer creation tools.

**What we need a full specification for:**

- **Offer types:** What categories of offers should the system support?
  - Subscription packages (recurring plans with feature tiers)
  - Credit bundles (one-time purchase of X credits at a discount)
  - Promotional offers (time-limited discounts or bonus credits)
  - Any other types?

- **Offer creation & management (super admin side):**
  - What fields define an offer? (Name, description, price, duration, credit amount, feature access, etc.)
  - Can offers be scheduled to activate/expire automatically?
  - Can offers be duplicated or templated?

- **Targeting & filtering:**
  - How should offers be targeted to specific companies? Possible filters could include:
    - Company size / tier / industry
    - Registration date or account age
    - Current subscription level
    - Geographic location
    - Manual company selection
  - Can a company receive multiple active offers simultaneously?
  - Should companies be notified when a new offer is available to them?

- **Subscription management:**
  - Can companies upgrade/downgrade mid-cycle? How is proration handled?
  - What happens when a subscription expires and is not renewed?
  - Is there a grace period?

**Design deliverables needed:**
- Offer management CRUD screens (super admin — create, edit, list, duplicate)
- Offer targeting/filter builder UI (super admin)
- Offer display on company side (we have promotional offer cards already — do they need redesign for new offer types?)
- Subscription plan comparison/selection screen (company side)
- Subscription upgrade/downgrade flow
- Offer notification design (in-app banner, notification center entry, or both?)

---

## Summary of Blocking Dependencies

| Module                              | Status                      | Needs from Product              | Needs from Design                                  |
| ----------------------------------- | --------------------------- | ------------------------------- | -------------------------------------------------- |
| Super Admin — Company Management    | Placeholder page            | CRUD scope, approval workflows  | List view, detail screen, edit form, status flows  |
| Payment — Stripe Integration        | UI built, no backend wiring | Payment method/flow decisions   | Checkout flow, failure/retry screens               |
| Payment — Withdrawals               | Not started                 | Confirm if needed + approval flow | Request form, status tracker, approval queue       |
| Payment — Manual Adjustments        | Not started                 | Confirm if needed + audit rules | Adjustment form (super admin)                      |
| Super Admin — Tariff Management     | Placeholder page            | Full spec (depends on Offers)   | CRUD screens, assignment UI                        |
| Schedule — Admin Oversight          | Not started                 | Scope of super admin access     | Cross-company overview, override UI                |
| Content Reporting                   | Not started                 | Separate module vs. tickets     | Report queue or ticket integration screens         |
| Offer Module                        | Not started                 | Full spec (types, targeting)    | CRUD screens, filter builder, company-facing cards |

---

We'd like to schedule a meeting or async review to go through these items. Product decisions will determine architecture and implementation order. Design deliverables will unblock frontend development. Both are needed before the next development phase can proceed.

**Suggested next steps:**
1. Product team reviews and makes decisions on each section above
2. Design team receives confirmed specs and begins wireframes/mockups
3. Development team reviews designs and begins implementation
