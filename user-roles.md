# Campus Market — User Roles

<!-- WHAT IS A USER ROLE?
A user role defines who uses the product and what they are allowed to do.
Defining roles before you build prevents mistakes — for example, building
a screen that any user can access when it should only be available to an administrator.
The AI agent reads this file to know what to allow and what to restrict. -->

Three roles use Campus Marketplace. Every feature belongs to one or more of them.

## Role overview

| Role | Who they are | Typical number |
|---|---|---|
| **Buyer (Student)** | A student who browses and purchases items | Unlimited |
| **Seller (Student)** | A student who lists items for sale | Unlimited |
| **Admin (Coordinator)** | A student moderator who ensures platform safety | 1–2 per campus |

*Note: A single student can be both a buyer and a seller. Permissions are additive.*

---

## Buyer

**Goal:** Find and purchase needed items quickly and safely.

**Can do:**
- Browse the shared feed of all available items (chronological or ranked)
- Search by keyword and filter by category (textbooks, electronics, furniture, food, etc.)
- View full product details: photos, price, description, seller info
- Contact a seller via in-app direct messaging (real‑time chat)
- Request an offline meet‑up with location preference (dormitory or campus building)
- Report a suspicious or rule‑violating product listing
- Mark an order as “received” after completing the offline transaction

**Cannot do:**
- Edit or delete any product listing (only the seller can)
- Access moderation tools (reported items list, user management)
- Bypass campus‑only authentication

---

## Seller

**Goal:** List items for sale quickly and manage active listings.

**Can do:**
- Create a product listing with title, description, category, price, and 1–5 images
- Edit or deactivate their own active listings
- Mark a product as “sold” (removes it from the marketplace feed)
- Receive and respond to buyer messages via in‑app chat
- View and accept/decline meet‑up requests from buyers
- View their own sold and active listings in a personal dashboard

**Cannot do:**
- Modify or delete another user’s listings
- Report a product (reporting is a buyer action – but sellers can still report if they act as buyers)
- Access admin moderation features

---

## Admin (Coordinator)

**Goal:** Maintain platform safety, handle reported content, and manage user accounts.

The admin is also a student (buyer/seller). All buyer and seller permissions apply. The admin has additional privileges on top.

**Additional permissions:**
- Access the admin dashboard: view all reported products and user reports
- Dismiss a report (if the listing is compliant)
- Delete a reported product listing (if it violates rules)
- View all user accounts (student IDs, registration dates)
- Manually deactivate suspicious user accounts

**Cannot do:**
- Edit or delete any user’s private messages (chat history is append‑only)
- Bypass the same campus‑only authentication (admin must also be a verified student)
- Access financial or payment data (no online payments exist)

---