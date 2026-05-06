# Campus Market — Product Requirements

<!-- WHAT IS THIS FILE?
This file describes what Campus Market is, who uses it, and what it must do.
It is the main context file for your AI coding agent — read it first at the
start of every session. It answers:
  1. What problem are we solving?
  2. Who are the users and what are their goals?
  3. What must the product do — and what must it NOT do? -->

---

## What it is

Campus Market is a mobile web app for students at XJTLU to buy, sell, and give away second‑hand goods and food items.

All transactions are arranged via **offline meet‑ups** on campus. The platform handles listings, search, chat, and meet‑up requests, while the actual exchange of goods and payment happens face‑to‑face between students.

<!-- WHAT IS A MOBILE WEB APP?
A mobile web app is a website designed to look and feel like an app on your phone.
Users open it in their browser (Safari, Chrome, or the WeChat browser) — no download needed.
It is different from a native app (like WeChat or TikTok) which must be installed. -->

---

## The problem

Students at XJTLU currently have no dedicated platform to trade used items or share food. They rely on scattered WeChat group chats, which cause three specific problems:

1. **No discoverability.** Listings get buried in endless chat messages. Sellers cannot reach buyers effectively, and buyers cannot easily find what they need — especially small quantities of food or specific textbooks.
2. **No accountability.** There is no way to track which listings are still active. Outdated posts clutter the feed, and students waste time messaging about already‑sold items.
3. **No safety.** Transactions happen in unregulated group chats with no verification that the other person is actually a student on the same campus. This creates trust and security risks.

The result: usable items go to waste, students overpay for new goods, and unsafe transactions threaten student safety.

---

## Users

Full role definitions and permission rules are in `user-roles.md`.

| Role | Primary goal | How many |
|---|---|---|
| **Buyer (Student)** | Find and purchase items quickly and safely | Unlimited |
| **Seller (Student)** | List an item for sale in under 2 minutes; manage active listings | Unlimited |
| **Admin (Coordinator)** | Moderate reported listings; ensure platform safety | 1–2 per campus |

Most users are undergraduate students on an iPhone or Android phone, with valid XJTLU email addresses used for campus‑only authentication.

---

## Core requirements

These are the things the product MUST do. Build these before anything else.
Do not move on to optional features until every item here works end‑to‑end.

| # | Requirement | Role |
|---|---|---|
| R1 | Student can register/login using XJTLU email domain whitelist or SSO | All |
| R2 | Student can browse a shared feed of all available items (chronological or ranked) | Buyer |
| R3 | Student can search by keyword and filter by category (textbooks, electronics, furniture, food, etc.) | Buyer |
| R4 | Student can view full product details: photos, price, description, seller info | Buyer |
| R5 | Seller can create a product listing with title, description, category, price, and 1–5 images in under 2 minutes | Seller |
| R6 | Buyer can contact seller via in‑app direct messaging (real‑time chat) | Buyer |
| R7 | Buyer can request an offline meet‑up with location preference (dormitory or campus building) | Buyer |
| R8 | Seller can mark a product as “sold”; sold products are removed from the marketplace feed | Seller |
| R9 | Student can report a suspicious or rule‑violating product listing; same user cannot report same product twice | All |
| R10 | Admin can view reported products and take action (dismiss report or delete listing) | Admin |

---

## Constraints

These apply to every feature. The AI agent must treat these as hard limits.

| Constraint | Detail |
|---|---|
| **Mobile‑first** | Every screen is designed for a 390px wide phone viewport. Desktop is secondary. |
| **Campus‑only authentication** | Registration requires a valid XJTLU email address or SSO to ensure only campus users access the platform. |
| **No online payment** | Platform handles listings, chat, and meet‑up coordination only. Payment and goods exchange happen offline between buyer and seller. Do not build any payment features. |
| **No real‑time recommendations in MVP** | Personalized recommendations are a stretch goal. The MVP relies on search and category filters. |
| **Simple messaging** | Real‑time chat with WebSocket is optional for MVP; simple polling or email notifications can be used initially. |
| **Append‑only moderation** | Reported items and user actions are logged. Admin can delete listings, but the report record remains. |
| **Runs in the browser** | No app to install. The product opens as a URL and works in Safari, Chrome, and the WeChat in‑app browser. |
| **Free tier only** | All tools must have a free tier sufficient for expected student usage: hundreds of listings and thousands of page views per week. |
| **Chinese text support** | Product titles, descriptions, and chat messages are often in Chinese. The app must display Chinese characters correctly. |

---

## Out of scope

Do not build these. If a user story seems to require one of them, ask for clarification.

| Out of scope | Reason |
|---|---|
| Online payment integration (WeChat Pay, Alipay, etc.) | Transactions happen offline via meet‑up |
| Delivery or shipping logistics | All transactions are face‑to‑face on campus |
| Rating or review system for users | Out of initial scope; may be added later |
| Personalized recommendation algorithm | Stretch goal — not required for MVP |
| Native mobile app (iOS / Android) | Mobile browser is sufficient; no App Store deployment |
| Advanced admin dashboard beyond basic moderation | Use direct database access or simple admin panel |
| Offline mode or data sync | The app requires an internet connection |
| Multi‑campus support (Suzhou + Taicang) | One campus (Suzhou) for MVP |
| Public access | Only verified XJTLU students can register and use the platform |

---

## Definition of done

The product is ready to present when:

- [x] All 10 core requirements (R1–R10) work end‑to‑end on a real mobile device
- [x] At least 5 validation sessions are documented in the Validation Report
- [x] The Technical Documentation describes the architecture, stack choices, and data model
- [x] The app is deployed to a public URL that any assessor can open on their phone
