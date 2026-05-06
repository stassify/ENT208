# Campus Market — UI Specification

<!-- WHAT IS A UI SPEC?
A UI spec (User Interface Specification) describes what the app looks like and
how it behaves. A developer uses it to make decisions about colour, layout, and
interaction without guessing. An AI coding agent uses it as context to generate
code that matches your visual style — not a generic default. -->

This document defines the visual language, component styles, layout rules, and interaction patterns for the Campus Market web app. 
---

## App identity

Campus Market is a **second-hand trading and food selling platform** for students at Xi’an Jiaotong-Liverpool University (XJTLU), Suzhou.

**Design character:**  
Modern, clean, and trustworthy. The deep green primary colour conveys reliability and campus vitality. The interface is mobile-first, spacious, and touch-friendly.

**Not:** Cluttered, corporate grey, form-heavy, or slow.  
**Yes:** Fast actions, large touch targets, clear feedback, consistent spacing.

The app supports both English and Chinese (i18n via `src/i18n`). UI text follows the user’s language preference, while product titles and descriptions can be in either language.

---

## Colour system

Colours are defined in `index.css` using HSL variables. Dark mode is defined (`.dark` class) but no theme switcher is implemented; the app currently uses light mode only.

### Light Mode (default)

| CSS Variable | HSL Value | Usage |
|--------------|-----------|-------|
| `--background` | `210 20% 97%` | Page background (light grey‑green) |
| `--foreground` | `150 30% 15%` | Primary text (dark grey‑green) |
| `--primary` | `150 30% 26%` | Brand colour (deep green) |
| `--primary-foreground` | `0 0% 100%` | Text on primary buttons (white) |
| `--secondary` | `210 15% 92%` | Secondary button background |
| `--secondary-foreground` | `150 30% 15%` | Text on secondary buttons |
| `--muted` | `210 15% 92%` | Muted backgrounds (e.g., input fields) |
| `--muted-foreground` | `150 10% 45%` | Hints, timestamps, secondary labels |
| `--accent` | `210 20% 95%` | Subtle emphasis backgrounds |
| `--accent-foreground` | `150 30% 15%` | Text on accent backgrounds |
| `--destructive` | `5 75% 55%` | Danger actions (red) |
| `--destructive-foreground` | `0 0% 100%` | Text on destructive buttons |
| `--border` | `210 15% 88%` | Card borders, dividers |
| `--input` | `210 15% 88%` | Input field background |
| `--card` | `0 0% 100%` | Card background |
| `--card-foreground` | `150 30% 15%` | Card text |
| `--ring` | `150 30% 26%` | Focus ring (same as primary) |

**Colour usage rules:**
- Primary (green) appears on main action buttons: “Buy Now”, “Publish”, “Save Preferences”. One green button per screen.
- Destructive (red) is used for “Deactivate”, “Cancel”, “Remove” actions.
- Muted colours are used for secondary information and non‑interactive elements.
- Borders and dividers use `--border` (light grey).


---

## Typography

### Font Family

The app relies on Tailwind’s default `sans` stack. No external fonts are loaded.

```css
font-family: system-ui, -apple-system, 'Segoe UI', 'PingFang SC', 'Microsoft YaHei', sans-serif;
This ensures fast loading and correct rendering of both English and Chinese characters.
PingFang SC (iOS/macOS) and Microsoft YaHei (Windows) are preferred for Chinese text.

### Type Scale

| Usage | Size | Weight | Example |
|-------|------|--------|---------|
| Captions, timestamps | 12px (0.75rem) | 400 | “2 minutes ago” |
| Secondary info, seller ID | 14px (0.875rem) | 400 | “Seller: 21***45” |
| Body text, form labels | 16px (1rem) | 500 | “Product title” |
| Card titles, section headers | 18px (1.125rem) | 600 | “Textbook for sale” |
| Page titles | 24px (1.5rem) | 700 | “My Orders” |
| Price | 20px (1.25rem) or 24px | 700 | `¥29.99` (coloured primary) |

All text uses the `foreground` variable for default colour and `muted-foreground` for secondary labels.

---

## Layout Principles

### Mobile-First
- Base design width: 390px (iPhone 14).  
- Use Tailwind’s responsive grid: `grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4` for product grids.  
- Main container: `container mx-auto px-4 py-6 max-w-4xl` (desktop limit) or `max-w-2xl` for conversation pages.

### Spacing
- Based on 4px unit (Tailwind’s default scale).  
- Common values: `gap-2` (8px), `p-4` (16px), `space-y-4` (16px), `py-6` (24px), `mb-6` (24px).

### Touch Targets
- Any interactive element (button, card, list item) must be at least 44px tall.  
- Buttons use `h-10` (40px) or `h-12` (48px).  
- Icon buttons use `p-2` (32px) with `min-width: 44px`.

### Navigation
- **No bottom tab bar.** Main navigation is through the profile menu (`ProfilePage`) and header back buttons.  
- The home page uses a sticky search bar + category filter.  
- Return navigation: `<Button variant="ghost" onClick={() => navigate(-1)}>` with `ArrowLeft` icon.

### Safe Areas
iPhones with notches are handled by Tailwind’s `env(safe-area-inset-top)` automatically on the root element.  
For custom full‑screen elements, add `pt-safe` or `pb-safe` utilities if needed (not currently required).


---

## Key Screens
---

## Screen 1 — Home (Product List)

**Purpose:** Let students browse all active listings at a glance, discover personalised recommendations, and filter by category.

**Layout:**

```
┌──────────────────────────────────────────────────────────┐
│ 🎓 Campus Market  Home  [Graduation Sale]  Publish       │
│                         Orders  Profile  [🌐]  [avatar]  │  <- top nav bar
├──────────────────────────────────────────────────────────┤
│ ┌──────────────────────────────────────────────────────┐ │
│ │ Search products...                                   │ │  <- full-width search bar
│ └──────────────────────────────────────────────────────┘ │
│                                                          │
│  [All] [Second-hand] [Food] [Study Supplies]             │  <- category filter chips
│  [Digital Products] [Sports & Fitness]                   │
│  [Daily Necessities] [Entertainment] [Others]            │
│                                                          │
│  Products recommended based on your preferences          │  <- section header
│                                                          │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐   │
│  │Grad Sale │ │Grad Sale │ │Grad Sale │ │Grad Sale │   │  <- product cards, 4-col grid
│  │ [photo]  │ │ [photo]  │ │ [photo]  │ │ [photo]  │   │
│  │ Rolling  │ │  canon   │ │glass jar │ │dji pocket│   │
│  │ Storage  │ │          │ │set(2jars)│ │    3     │   │
│  │ Trolley  │ │          │ │          │ │          │   │
│  │ ¥20.00   │ │ ¥3000.00 │ │  ¥15.00  │ │ ¥1500.00 │   │
│  │Secondhand│ │Secondhand│ │Secondhand│ │  Digital │   │
│  │123  2026/5│ │Unknown 5/5│ │123  2026/5│ │Unknown 5/5│  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘   │
│                                                          │
│  [ second row of cards ... ]                             │
└──────────────────────────────────────────────────────────┘
```

**Key behaviours:**
- The recommendation section is driven by the user's saved preference categories (set in Profile -> My Preferences). It is visible only when the user is logged in and has at least one preference category selected.
- Category filter chips are single-select. Selecting a chip filters the product grid in place without a full page reload. "All" is selected and highlighted by default.
- Each product card displays: product photo, title, price, category tag, seller ID, and listing date.
- Products tagged as Graduation Sale show an orange "Grad Sale" badge in the top-left corner of the card image.
- Empty state (no results for the selected filter): "No products found in this category. Try a different one!"

**Components / elements:** top nav bar, search bar, category filter chips, product card grid, Grad Sale badge overlay.

---

## Screen 2 — Graduation Sale

**Purpose:** A dedicated page aggregating all Graduation Sale listings, with a hero banner to create urgency and encourage graduating students to publish.

**Layout:**

```
┌──────────────────────────────────────────────────────────┐
│ [top nav bar -- same as home]                            │
├──────────────────────────────────────────────────────────┤
│ ┌──────────────────────────────────────────────────────┐ │
│ │  Graduation Sale                  (Limited Time)     │ │  <- hero banner, orange gradient
│ │  Limited Time Deals . End of School Clearance        │ │
│ │  Quality items from graduating students              │ │
│ │  -- grab them before they're gone!                   │ │
│ │                                                      │ │
│ │  [ Search graduation sale items... ]  [Sell Your Items] │ <- search + CTA button
│ └──────────────────────────────────────────────────────┘ │
│                                                          │
│  Graduation Sale . 5 items                               │
│  Graduation season deals -- first come, first served     │
│                                                          │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐   │
│  │Grad Sale │ │Grad Sale │ │Grad Sale │ │Grad Sale │   │  <- same card component as home
│  │ [photo]  │ │ [photo]  │ │ [photo]  │ │ [photo]  │   │
│  │ Rolling  │ │  canon   │ │dji pocket│ │glass jar │   │
│  │ Storage  │ │          │ │    3     │ │set(2jars)│   │
│  │ Trolley  │ │          │ │          │ │          │   │
│  │ ¥20.00   │ │ ¥3000.00 │ │ ¥1500.00 │ │  ¥15.00  │   │
│  │Secondhand│ │Secondhand│ │  Digital │ │Secondhand│   │
│  │123  2026/5│ │Unknown 5/5│ │Unknown 5/5│ │123  2026/5│  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘   │
│                                                          │
│  [ fifth card partially visible, scroll to see more ]    │
└──────────────────────────────────────────────────────────┘
```

**Key behaviours:**
- The hero banner uses an orange-to-amber gradient background with white text.
- The "Sell Your Items" button navigates to the Publish Product page with the "Graduation Sale" listing type pre-selected.
- The item count ("5 items") reflects the real-time total of active Graduation Sale listings pulled from the database.
- The grid is sorted by listing date descending (newest first) by default.
- Empty state: "No Graduation Sale items yet. Be the first to list one!"

**Components / elements:** top nav bar, hero banner, inline search bar, "Sell Your Items" CTA button, item count label, product card grid (shared component with home).

---

## Screen 3 — Publish Product

**Purpose:** Let a student create a new product listing. The form covers all required listing details. The listing type (Normal or Graduation Sale) is chosen at the top of the form.

**Layout:**

```
┌──────────────────────────────────────────────────────────┐
│ [top nav bar]                                            │
│ <- Back                                                  │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  Publish Product                                         │  <- page title
│  Fill in product information and upload images           │  <- subtitle
│                                                          │
│  Publish Type *                                          │
│  ┌──────────────────────────┐ ┌──────────────────────┐  │
│  │ [house icon]  Normal  (o)│ │[grad icon] Grad Sale │  │  <- two type selector cards
│  │ Product will appear in   │ │ Appears in regular   │  │
│  │ regular listings         │ │ AND Graduation Sale  │  │
│  │                          │ │ with priority place- │  │
│  │                          │ │ ment                 │  │
│  │                          │ │ * Priority Boost     │  │
│  └──────────────────────────┘ └──────────────────────┘  │
│                                                          │
│  Product Title *                                         │
│  [ Enter product title                               ]   │  <- text input
│                                                          │
│  Category *                                              │
│  (o) Second-hand        ( ) Food                         │
│  ( ) Study Supplies     ( ) Digital                      │  <- radio button grid, 2 columns
│  ( ) Sports             ( ) Daily                        │
│  ( ) Entertainment      ( ) Others                       │
│                                                          │
│  Description *                                           │
│  [ Describe your product...                          ]   │  <- multi-line textarea
│  [                                                   ]   │
│  [                                                   ]   │
│                                                          │
│  Price (Y) *                                             │
│  [ Enter price                                       ]   │  <- number input
│                                                          │
│  Images (1-5) *                                          │
│  [ +-  drag & drop or click to upload images         ]   │  <- image upload zone
│                                                          │
│  ┌──────────────────────────────────────────────────┐    │
│  │                    Publish                       │    │  <- primary button, full-width
│  └──────────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────────┘
```

**Key behaviours:**
- **Publish Type** is a required selection between two styled cards: "Normal" and "Graduation Sale". Only one can be active at a time. The active card shows a filled radio indicator and a highlighted border.
- Selecting "Graduation Sale" reveals the "Priority Boost" label inside that card, communicating the placement benefit to the seller.
- If the user arrives from the Graduation Sale page's "Sell Your Items" button, the "Graduation Sale" card is pre-selected.
- All fields marked with * are required. The "Publish" button is disabled until all required fields have valid values and at least one image has been uploaded.
- **Images:** 1 to 5 photos are allowed per listing. The upload zone accepts both drag-and-drop and file picker. Uploaded photos appear as thumbnails with an individual remove button on each.
- On successful submit, the user is redirected to the newly created product's detail page.
- On failure (e.g. network error or validation error), an inline error message appears below the affected field in red.

**Components / elements:** back link, publish type selector cards, product title input, category radio grid, description textarea, price number input, image upload zone, submit button.

---

## Screen 4 — Profile

**Purpose:** Let a student manage their account, configure recommendation preferences, and review or manage their own listings.

**Layout:**

```
┌──────────────────────────────────────────────────────────┐
│ [top nav bar]                                            │
├──────────────────────────────────────────────────────────┤
│  ┌──────┐  123                                           │
│  │  12  │  Student                                       │  <- avatar + username + role
│  └──────┘                                               │
│                                                          │
│  ┌──────────────────────────────────────────────────┐    │
│  │  My Orders                                       │    │
│  │  My Favorites                                    │    │
│  │  My Messages                                     │    │  <- account menu rows
│  │  Message Center                                  │    │
│  │  Logout                                          │    │
│  └──────────────────────────────────────────────────┘    │
│                                                          │
│  ┌──────────────────────────────────────────────────┐    │
│  │ My Preferences                  [Edit Preferences]│   │  <- preference section
│  │ Preferred Categories:                            │    │
│  │ [Second-hand]  [Food]                            │    │
│  │ Keywords: Not set                                │    │
│  └──────────────────────────────────────────────────┘    │
│                                                          │
│  ┌──────────────────────────────────────────────────┐    │
│  │ My Products                           [Publish]  │    │  <- my listings section
│  │                                                  │    │
│  │  [photo]  bag                      [On Sale]     │    │
│  │           Y20.00            [View] [Deactivate]  │    │
│  │                                                  │    │
│  │  [photo]  Tape-newjeans            [On Sale]     │    │
│  │           Yxx.xx            [View] [Deactivate]  │    │
│  └──────────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────────┘
```

**Key behaviours:**
- **My Preferences:** Tapping "Edit Preferences" opens an edit panel where the user can toggle category chips on or off and enter free-text keywords. Changes saved here immediately update the recommendation feed shown on the Home page.
- **My Products:** Lists all items the user has published, each showing a thumbnail, title, price, status badge, and two action buttons.
  - **View** -- navigates to the product detail page in seller view.
  - **Deactivate** -- shows a confirmation dialog before delisting. Once confirmed, the status badge changes to "Deactivated" and the listing is removed from public browsing.
- **My Orders** -- links to a separate order history page.
- **My Messages** -- links to the in-app chat thread list.
- **Message Center** -- displays system notifications such as order updates and admin notices.
- **Logout** -- shows a confirmation dialog before logging the user out.
- Empty state for My Products: "You have not listed any products yet. Tap Publish to get started!"

**Components / elements:** avatar, username and role label, account menu list, preference category tags, keyword display, "Edit Preferences" button, product list rows with status badge and action buttons, "Publish" shortcut button.

---

## Interaction Patterns

### Click feedback
All clickable elements give immediate visual feedback. For custom clickable cards (e.g. product cards):
```css
.clickable:active {
  transform: scale(0.97);
  transition: transform 0.1s ease-out;
}
```

### Form validation
Required fields are marked with an asterisk (*). Validation runs on form submit.
Error messages appear inline directly below the field that failed, in red text.
The submit button is disabled until all required fields have valid values.

### Confirmation dialogs
Destructive or irreversible actions (Deactivate listing, Logout) always show a confirmation dialog first.
The dialog contains two buttons: "Cancel" (secondary, outlined) and a confirm button (primary, coloured to match the severity of the action).

### Success banner
After a successful action (publish, deactivation), a green banner slides in from the top:
```css
.confirm-banner {
  background: #4caf50;
  color: #fff;
  padding: 12px 16px;
  font-weight: 600;
  animation: slide-down 0.25s ease-out;
}
@keyframes slide-down {
  from { transform: translateY(-100%); opacity: 0; }
  to   { transform: translateY(0);     opacity: 1; }
}
```
The banner auto-dismisses after 2500 ms.

---

## Empty States

Every list view must display a meaningful empty state rather than a blank area.

| Screen | Empty state message |
|---|---|
| Home -- all categories | "No products listed yet. Check back soon!" |
| Home -- filtered category | "No products found in this category. Try a different one!" |
| Graduation Sale | "No Graduation Sale items yet. Be the first to list one!" |
| My Products | "You have not listed any products yet. Tap Publish to get started!" |
| My Favorites | "No saved items yet. Tap the heart icon on any product to save it." |
| My Orders | "No orders yet. Browse the marketplace to find something you like!" |

---

## Accessibility Checklist

- [x] All icon-only buttons include an aria-label describing their action
- [x] All form fields have a visible label linked by for / id attributes
- [x] Text colour contrast meets WCAG AA (minimum 4.5:1 ratio for body text)
- [x] Status information (On Sale, Grad Sale badge) is never conveyed by colour alone -- always paired with a text label
- [x] All interactive elements have a minimum click / touch target size of 44 x 44 px
- [x] The layout reflows correctly when the browser default font size is increased
