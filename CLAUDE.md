# Aigis — Interactive Mockup Web App

## What this is

Aigis is a browser extension / browser UI concept designed for seniors. It combines a
simplified browsing experience with AI-powered scam detection, safe online shopping, and
form autofill. This codebase is an interactive HTML/CSS/JS mockup (no backend) used to
demonstrate two key path scenarios for a university HCI course (CS486, EPFL).

The app should look and feel like a desktop browser window running inside a webpage.

---

## Visual design reference

The attached screenshot (`AIrgus.png`) is the reference design. Reproduce it faithfully:

- **Window chrome**: dark grey top bar (#2b2b2b) with three macOS-style traffic light
  circles (red #ff5f57, yellow #ffbd2e, green #28c840) on the top left. Back/forward
  arrows and a reload icon follow them.
- **Left sidebar** (width ~230px, light grey #f0f0f0): two sections separated by a thin
  divider. Top section labeled "Shortcuts / Quickly access" lists pinned destinations
  (Gertrude's Mail, Facebook, SafeShop) each with an icon, a bold label, and a muted
  subtitle. Bottom section labeled "Open Tabs / Currently Looking at" lists open tabs.
  Active tab has a small tag icon.
- **Center content area** (flex-grow, white background): on the home/welcome screen shows
  a large bold greeting "Welcome Gertrude!" with subtitle "What will it be today?" and a
  centered search bar with a search icon and a microphone icon on the right.
- **Right AI panel** (width ~420px, very light grey #f5f5f5): persistent chatbot sidebar.
  Chat bubbles appear in the upper area. User messages align right (white bubble), AI
  messages align left with a small robot icon. Bottom input bar has an image icon, a code
  icon, and a mic icon, plus a send button (dark circle with arrow).
- **Typography**: use a clean, large, highly readable font. Suggested: `DM Sans` or
  `Nunito` from Google Fonts. Minimum body size 15px. Headings 28px+.
- **Colors**: keep the UI calm and low-contrast. Trust indicators use green (#34c759) for
  safe and red/orange (#ff3b30 / #ff9500) for suspicious. No purple gradients. No dark
  mode for content areas (seniors need high contrast on white).

---

## Screens to implement

Build a single HTML file with JavaScript managing screen state. Each "screen" is a view
that replaces the center content area (the sidebar and AI panel stay visible at all times).

### Screen 0 — Home / Welcome (default)
- Large greeting, search bar with mic button, nothing else in center.

### Screen 1 — SafeShop: search results (chat mode)
Triggered when user clicks "SafeShop" in the sidebar.
- Center area becomes a chat interface mirroring the right AI panel style but wider.
- First AI message: "What are you looking for today? You can type or use the mic."
- Show a mic button prominently.
- After a simulated user message ("A pink nightstand"), show AI typing indicator (animated
  dots), then AI response with follow-up question: "Would you like to answer a few more
  questions to refine the results, or shall I show you what I found?"
- Two large buttons: "Show results" and "Add details".

### Screen 2 — SafeShop: product results
Triggered after "Show results" is clicked.
- Grid of 2-3 product cards. Each card has:
  - Product image (use placeholder via https://placehold.co)
  - Product name and price
  - A safety score badge: green shield for 100%, orange for 90%, etc.
- One card has a 90% score. It has a "More info" button.
- Clicking "More info" expands the card to show: "This item is sold by a reseller on
  TheGoodCorner which has some negative reviews."
- An "Other results" button at the bottom.

### Screen 3 — SafeShop: cart confirmation popup
Triggered when "Add to cart" is clicked on a product, then "Checkout".
- A modal overlay with a summary: item name, price, delivery address, payment method
  (last 4 digits only).
- Two buttons: grey "Go back", green "Confirm purchase".
- After confirm: success message in AI panel "Payment successful! Your nightstand should
  arrive in 3 to 5 business days."

### Screen 4 — Mail: inbox
Triggered when user clicks "Gertrude's Mail" in the sidebar.
- List of email previews. Each has a subtle background tint:
  - Red/orange tint: suspicious email ("Your account has been suspended — BNP Paribas")
  - Green tint: safe emails (tax office reminder, doctor confirmation)
- Clicking the suspicious email opens Screen 5.
- Clicking the tax email opens Screen 6.

### Screen 5 — Mail: scam email open
- Email content visible. When the link inside is hovered/clicked, a popup appears:
  "Warning: this link leads to a website flagged in multiple scam databases."
- "More info" button and "Go back" button.
- Clicking "More info" shows explanation. Clicking "Understood" dismisses popup, returns
  to inbox, and shows a short note below the email list: "Your real bank will never ask
  you to verify your account by clicking a link in an email."

### Screen 6 — Mail: tax email + autofill form
- Tax email open with a safe link. Hovering the link shows a small green checkmark.
- Clicking the link opens the tax form in a new view (still inside Aigis center area).
- AI panel shows: "Would you like me to fill this form for you?" with a "Yes please"
  button.
- Clicking yes fills all fields (show them turning green one by one with a brief animation).
- One field stays empty and highlighted yellow. A popup explains what is needed and has
  an "Import document" button (simulate with a file input or a fake browse dialog).
- After import: field fills in green. AI panel shows a "Review before sending" prompt.
- Clicking review shows a plain-language summary modal. "Send" button completes the flow.
- Success screen: "Your taxes have been submitted. Well done!"

---

## Interaction rules

- The left sidebar is always visible and clickable to switch between screens.
- The right AI panel is always visible. Its content updates contextually per screen.
- No real backend. All data is hardcoded or simulated with setTimeout.
- All transitions between screens should be smooth (CSS fade or slide, 200ms).
- Popups and modals use a dark overlay backdrop.
- Every destructive or irreversible action (confirm purchase, send taxes) requires a
  confirmation step before completing.
- The mic button is visual only (no real speech recognition needed for the mockup).

---

## Technical constraints

- Single HTML file preferred (inline CSS and JS).
- No frameworks required, but React or Vue are acceptable if it helps.
- Use Google Fonts (DM Sans or Nunito).
- No external API calls.
- Must render correctly at 1280x800 minimum viewport.
- Accessibility: all buttons must have visible focus states and descriptive labels.

---

## File structure (if multi-file)

```
aigis-mockup/
  index.html       # main entry point
  style.css        # global styles (optional if inlined)
  app.js           # screen state logic (optional if inlined)
  AIrgus.png       # reference screenshot (do not modify)
```

---

## What to avoid

- Do not add a login or registration screen.
- Do not use purple gradients or dark-mode content areas.
- Do not use tiny fonts. Gertrude is a senior: minimum 15px body, 18px+ for form labels.
- Do not show raw URLs or technical error messages to the user.
- Do not add features not listed above. Keep scope to the two KPS flows.
