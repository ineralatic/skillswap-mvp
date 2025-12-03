# SkillSwap MVP Design Guidelines

## Design Approach

**Reference-Based Approach**: Drawing inspiration from Linear (clean productivity), Notion (information-dense cards), and modern glassmorphism trends. The dark glass aesthetic with gradient accents creates a premium, focused experience for skill matching and scheduling.

**Core Principle**: Information density with clarity - users need to quickly scan profiles, evaluate recommendations, and schedule sessions without cognitive overload.

---

## Typography System

**Font Family**: 
- Primary: Inter or DM Sans (via Google Fonts CDN)
- Monospace: JetBrains Mono (for IDs, technical details if needed)

**Hierarchy**:
- Hero/Page Titles: text-3xl to text-4xl, font-semibold
- Section Headers: text-xl to text-2xl, font-medium
- Card Titles: text-lg, font-semibold
- Body Text: text-base (16px), font-normal
- Metadata/Labels: text-sm (14px), font-medium
- XAI Explanations: text-sm, font-normal, reduced opacity
- Micro-text (badges, timestamps): text-xs (12px)

---

## Layout & Spacing System

**Tailwind Spacing Primitives**: Use units of **2, 3, 4, 6, 8, 12, 16** for consistency
- Component padding: p-4 to p-6
- Card spacing: gap-4 to gap-6
- Section margins: mb-8 to mb-12
- Page containers: max-w-6xl mx-auto px-4

**Grid System**:
- Recommendations: grid-cols-1 lg:grid-cols-2 gap-4
- Skill chips: flex flex-wrap gap-2
- Form layouts: Single column with max-w-2xl for focused data entry

---

## Component Library

### Navigation
- **Top Bar**: Fixed, backdrop-blur-md with subtle border-b, contains logo, main nav links (Profile, Recommendations, Schedule), user menu dropdown
- Height: h-16
- Nav items: text-sm font-medium with subtle hover states

### Cards & Containers
- **Glass Cards**: rounded-xl with backdrop-blur, subtle border (border-opacity-10), shadow-lg
- **Recommendation Cards**: Structured layout with:
  - Header: Profile name (text-lg font-semibold) + mode badge
  - Reputation: Star icon + numeric rating + count in muted text
  - XAI Section: Small text block with reduced opacity explaining match factors
  - Action Row: Two buttons (Accept/Decline) in button group
  - Padding: p-6, gap-3 between sections

- **Profile Cards**: Segmented sections for offered skills, wanted skills, availability with clear visual separation (border-t with reduced opacity)

### Form Elements
- **Inputs**: rounded-lg, px-4 py-2.5, backdrop-blur with translucent backgrounds
- **Labels**: text-sm font-medium, mb-2
- **Skill Selectors**: Multi-select with chip display, level slider (1-5) for offered skills
- **Availability Builder**: Weekday dropdown + time pickers + mode toggle + zone input in compact row layout

### Badges & Pills
- **Skill Chips**: rounded-full px-3 py-1 text-xs font-medium with subtle gradient backgrounds
- **Level Indicators**: Small circular badges (w-6 h-6) showing 1-5 numbers
- **Mode Badges**: "ONLINE" / "IN-PERSON" with distinct visual treatments (rounded-md px-2 py-1 text-xs)
- **Reputation Badges**: Icon + number combination in flex layout

### Buttons
- **Primary (Accept/Schedule)**: Gradient background, rounded-lg px-4 py-2.5 font-medium
- **Secondary (Decline)**: Translucent background with border, same padding
- **Ghost**: Minimal styling for tertiary actions
- **Blurred Backgrounds**: When overlaying images/gradients, use backdrop-blur-sm

### Icons
- **Library**: Heroicons (via CDN)
- **Usage**: 
  - Navigation: w-5 h-5
  - Form labels: w-4 h-4 inline
  - Badges: w-3.5 h-3.5
  - Reputation stars: w-4 h-4 filled

---

## Page-Specific Guidelines

### /profile (Profile Management)
- **Layout**: Single column form, max-w-2xl centered
- **Sections** (stacked with mb-8):
  1. **Profile Header**: Email (read-only, muted), Display Name input, Bio textarea (rows-4)
  2. **Offered Skills**: Multi-select dropdown + chip display with level sliders beneath each chip
  3. **Wanted Skills**: Multi-select dropdown + chip display (no levels)
  4. **Availability**: Dynamic list with Add/Remove rows (weekday, time range, mode, zone)
  5. **Visibility**: Radio group (Public/Limited/Private) with descriptions
  6. **Actions**: Save button (sticky bottom on mobile, inline on desktop)

### /recommendations (Top 5 Matches)
- **Filter Bar**: Sticky top-8, backdrop-blur glass card with chip toggles (Online Only, In-Person, Evenings)
- **Recommendation List**: 
  - Grid: lg:grid-cols-2 gap-4 (stacks on mobile)
  - Each card structure:
    - Profile name + mode badge (flex justify-between)
    - Reputation row: stars + "4.6/5 (9 sessions)"
    - XAI explanation: Border-l-2 with pl-3, italic text-sm, reduced opacity
    - Button row: Accept (primary gradient) + Decline (ghost), gap-2
  - Empty state: Centered with illustration placeholder comment, encouraging message

### /schedule (Session Booking)
- **Layout**: Centered card, max-w-lg
- **Form Structure** (gap-6):
  1. Target profile (read-only display if coming from recommendation)
  2. Date picker (calendar component with highlighted available days)
  3. Time range: Two dropdowns (From/To) in flex gap-3
  4. Mode: Toggle switch ONLINE ↔ IN-PERSON
  5. Zone/Link: Conditional input (shows based on mode)
  6. Note: Textarea (rows-3, optional)
  7. Reminders: Checkboxes in flex gap-4 (24h before, 2h before)
  8. Confirm button: Full width, gradient, font-semibold
- **Success State**: Replace form with confirmation message + session details card

---

## Interaction Patterns

- **Card Hover**: Subtle lift (translate-y-1) + shadow enhancement, no animations
- **Skill Chip Removal**: X icon appears on hover, click removes with simple fade
- **Form Validation**: Inline error messages below inputs (text-sm, error treatment)
- **Loading States**: Skeleton cards matching final layout structure
- **Toast Notifications**: Top-right position, glass card style, auto-dismiss 4s

---

## Accessibility
- Maintain WCAG AA contrast ratios despite dark theme (test with opacity adjustments)
- All interactive elements keyboard-navigable
- Form inputs with proper labels and aria-describedby for errors
- Focus rings: ring-2 with appropriate offset

---

## No Images Required
This is a data-driven application focused on profiles and matching. No hero images or decorative photography needed. Visual interest comes from glassmorphism, gradients, and well-structured information design.