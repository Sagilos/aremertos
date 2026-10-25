---
id: EXT_INT-accessibility
category: external_requirements
title: International Standard for digital accessibility
obligation: MUST
requirement_references: [WCAG]
internal_references: []
normative_vs_informative: normative
---

# WCAG 2.2 Level AA
### Perceivable (Information must be visible to their senses)
- **Text Alternatives**
  - Provide alt text for all non-text content (images, icons, buttons) so screen readers can describe them.
- **Captions & Audio Descriptions**
  - Provide synchronized captions for all prerecorded video and audio content.
- **Contrast Minimum**
  - Regular text must have a contrast ratio of at least 4.5:1 against its background. Large text (18pt+ or 14pt bold) must be at least 3:1.
- **Non-Text Contrast**
  - UI components (like borders around input fields, checkboxes, or focus indicators) must have a contrast ratio of at least 3:1 against adjacent colors.
- **Resize Text**
  - Users must be able to zoom text up to 200% without the text breaking, overlapping, or forcing horizontal scrolling.
- **Reflow**
  - Content must wrap dynamically down to a width of 320 pixels (standard mobile width) without requiring vertical and horizontal scrolling at the same time.

### Operable (Users must be able to navigate the interface)
- **Keyboard Navigable**
  - All functionality (buttons, links, forms, tabs) must be fully usable via a keyboard alone (no mouse required).
- **No Keyboard Trap**
  - If a user moves focus into a component (like a modal popup) using a keyboard, they must be able to exit that component using only the keyboard.
- **Bypass Blocks**
  - Provide a "Skip to Content" link at the very top of the page so keyboard users can skip repetitive header navigation menus.
- **Focus Order**
  - As a user tabs through the PWA, components must receive focus in a logical, predictable reading order.
- **Focus Visible**
  - Never hide the outline indicator. Any element currently selected via keyboard navigation must show a clear, visible focus border.
- **Target Size**
  - Pointer targets (buttons, touch areas) must be at least 24x24 CSS pixels, or have enough spacing around them to prevent accidental clicks.

### Understandable (The UI and operations must make sense)
- **Language of Page**
  - Declare the default language of the app in the HTML header (e.g., <html lang="en"> or <html lang="fr">) so screen readers use the correct accent.
- **Predictable Navigation**
  - Navigation links, menus, and sidebars must appear in the same relative order across every page of your PWA.
- **Error Identification & Suggestion**
  - If a user makes an error in a form input, the error must be clearly identified in text (not just color changes), and the app must provide explicit suggestions on how to fix it.
- **Accessible Authentication**
  - Critical for login screens. Cognitive function tests (like memorizing passwords or solving puzzles/CAPTCHAs) cannot be mandatory unless an alternative method (like web authn/biometrics or copy-paste) is fully supported.

### Robust (Works reliably across different browsers and assistive tech)
- **Name, Role, Value**
  - For custom PWA elements (like a custom toggle switch or dropdown), you must use proper ARIA attributes (e.g., role="checkbox", aria-checked="true") so screen readers understand what the element does and its current state.
- **Status Messages**
  - When a dynamic action happens without a page reload (e.g., "Item added to cart" or an asynchronous error popup), the message must be announced immediately by screen readers using live regions (role="status" or aria-live="polite").
