# Campus Market — User Stories

<!-- WHAT IS A USER STORY?
A user story describes one thing a real user needs to do.
Format: "As a [role], I want [action], so that [outcome]."
It focuses on the user's goal — not on how the code works. -->

<!-- WHAT ARE ACCEPTANCE CRITERIA?
Acceptance criteria are the things that must be true for a feature to count as finished.
They are your checklist — and your stop signal when working with an AI coding agent.
Paste them directly into your AI prompt: "Build this feature. Stop when all these
conditions are true." -->

---

## Story 1 — Browse the shared feed

**As a student (buyer),** I want to browse a chronological or ranked feed of all available items posted by other students, so that I can easily discover small‑quantity food items or second‑hand goods without searching through messy group chats or going to the supermarket.

**Acceptance criteria:**
- [x] The home page displays a list of product cards (image, title, price, seller)
- [x] Products are ordered by creation date (newest first) or by a simple ranking (e.g., recently active)
- [x] Each card shows a clear “sold” or “available” status
- [x] Tapping any card opens the full product detail page
- [x] The feed updates immediately when a new item is posted (no manual refresh needed)

---

## Story 2 — Search and filter products

**As a student (buyer),** I want to search by keyword and filter by category (textbooks, electronics, furniture, food, etc.), so that I can quickly find exactly what I need — especially appropriate calculus learning materials or other specific items.

**Acceptance criteria:**
- [x] A search bar is visible on the home page
- [x] Entering a keyword returns products whose title or description contains that word
- [x] Category filters (e.g., “Textbooks”, “Electronics”, “Food”) are available as buttons or a dropdown
- [x] Applying a filter shows only products from that category
- [x] Search and filter can be used together (e.g., “calculus” + “Textbooks” category)
- [x] If no results match, a friendly empty state message appears: “No products found. Try a different keyword.”

---

## Story 3 — Receive interest‑based recommendations (stretch goal)

**As a student (buyer),** I want the app to recommend food‑related or other items based on my browsing history or category preferences, so that I never miss relevant items that match my interests.

**Acceptance criteria:**
- [x] The feed includes a “Recommended for you” section (or interleaved recommendations)
- [x] Recommendations are based on simple rules: “because you viewed X” or previously clicked categories
- [x] Recommended items are clearly labelled as “Recommended”
- [x] Users can dismiss a recommendation (optional, stretch)
- [x] This feature is optional for MVP — build after Stories 1, 2, 4, 5, 6 are complete

---

## Story 4 — List an item in under 2 minutes

**As a seller (student),** I want to list an item with photos, price, and description in under 2 minutes, so that I can sell or give away items quickly — especially during graduation season when I need to clear out belongings.

**Acceptance criteria:**
- [x] A “Publish” or “Sell” button is visible in the app navigation
- [x] The listing form includes: title (required), description (required), category (dropdown), price (number, required), and image upload (1–5 images)
- [x] Image upload supports selection from camera or gallery
- [x] Images are automatically compressed (max 1MB per image)
- [x] After submitting, the product appears in the shared feed within 2 seconds
- [x] A success message appears: “✓ Your item has been listed”
- [x] The seller can view their active listings in a “My Listings” section

---

## Story 5 — Direct messaging between buyer and seller (simplified)

**As a student (buyer or seller),** I want to send direct messages to the other party within the app, so that I can discuss details, arrange meet‑up time and place, and avoid fragmented communication across multiple WeChat chats.

**Acceptance criteria:**
- [x] On a product detail page, a “Contact Seller” button opens a chat interface
- [x] The chat shows the product reference (image and title) at the top
- [x] Messages appear in real‑time (polling or WebSocket — WebSocket preferred)
- [x] Users can send text messages; images are optional (stretch)
- [x] Unread message counts are shown in the conversation list
- [x] Chat history is persisted and viewable for both parties
- [x] For MVP, simple polling every 2–3 seconds is acceptable if WebSocket is too complex

---

## Story 6 — Campus‑only authentication and safety

**As a student,** I want to see that only other students from my campus can access the platform, so that I feel safer and more trusting when transacting and avoid being defrauded by outsiders.

**Acceptance criteria:**
- [x] Registration requires a valid XJTLU email address (e.g., `@xjtlu.edu.cn`)
- [x] A verification email is sent to confirm ownership of the address, or the app uses university SSO (OAuth)
- [x] No user without a verified campus email can log in or access any authenticated page
- [x] Each user’s student ID is displayed in a masked format (e.g., “21***45”) on product cards and chats
- [x] The login page clearly states: “Only XJTLU students with a valid campus email can register”

---

## Story 7 — Keep the feed clean (product status management)

**As a user (buyer or seller),** I want the product listing page to remain simple and updated in a timely manner with the status of items, so that I can keep the feed clean and avoid outdated posts.

**Acceptance criteria:**
- [x] Sellers can mark an item as “Sold” directly from their “My Listings” page or product detail page
- [x] Once marked sold, the product no longer appears in the shared feed
- [x] The seller can also “Deactivate” a listing (e.g., if they changed their mind) without marking it sold
- [x] Buyers cannot see deactivated or sold products in search or feed
- [x] Sold/deactivated products remain in the seller’s history for reference but are hidden from others