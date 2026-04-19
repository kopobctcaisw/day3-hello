# Design System Specification: The Guided Authority

## 1. Overview & Creative North Star
**Creative North Star: "The Architectural Mentor"**
This design system moves away from the frantic, high-density aesthetics of typical tech startups. Instead, it embraces an editorial, high-end educational feel tailored for a mature audience (40s+). The experience must feel authoritative yet spacious. We achieve this through **intentional asymmetry**, **exaggerated white space**, and a **layered surface architecture** that mimics the tactile quality of a premium physical workspace.

The goal is "Guided Authority"—using large, confident typography and a deep, trust-inducing color palette to signal that the user is in capable hands. We are not just building a website; we are curating a learning environment that respects the user's time and visual comfort.

---

## 2. Colors: Depth through Tonal Shift
We utilize a sophisticated Teal and Charcoal palette. To maintain a premium feel, we strictly adhere to the following logic:

### The "No-Line" Rule
**Explicit Instruction:** Designers are prohibited from using 1px solid borders for sectioning or containment. Boundaries must be defined solely through background color shifts. Use `surface-container-low` (#f2f3f6) against a `surface` (#f8f9fc) background to define distinct content zones. This creates a "soft-edge" transition that is easier on the eyes and feels more modern than rigid grids.

### Surface Hierarchy & Nesting
Treat the UI as a series of physical layers. Use the Surface tiers to create natural depth:
*   **Base Layer:** `surface` (#f8f9fc) for the main background.
*   **Sectional Layer:** `surface-container-low` (#f2f3f6) for secondary content blocks.
*   **Interactive/Card Layer:** `surface-container-lowest` (#ffffff) for high-focus areas like lesson cards or input forms.
*   **The Glass & Gradient Rule:** For hero sections or high-impact Call-to-Actions, use a subtle linear gradient from `primary` (#005c55) to `primary_container` (#0f766e). This adds a "soul" to the color that flat hex codes cannot achieve.

### Signature Textures
For floating "AI Insight" widgets, use **Glassmorphism**: 
*   **Fill:** `surface_container_lowest` at 70% opacity.
*   **Effect:** 20px Backdrop Blur.
*   **Result:** A frosted-glass effect that lets the brand colors bleed through, softening the interface.

---

## 3. Typography: Editorial Authority
Typography is the primary vehicle for trust. We use a dual-font strategy to balance modern tech with classic readability.

*   **Display & Headline (Manrope):** Chosen for its geometric clarity and open apertures. 
    *   **Display-LG (3.5rem/56px):** Used for Hero statements. Keep line-height tight (1.1) to create a "block" of text that feels like a headline in a high-end magazine.
    *   **Headline-LG (2.0rem/32px):** Used for section starts.
*   **Body & Title (Public Sans):** A neutral, highly legible sans-serif that excels in long-form reading for users 40+.
    *   **Body-LG (1rem/16px):** The absolute minimum for body text. Never go smaller for instructional content.
    *   **Leading:** Set body line-height to 1.6. This "breathing room" is essential for cognitive ease in learning complex topics like AI coding.

---

## 4. Elevation & Depth: Tonal Layering
Traditional shadows are often "dirty" and clutter the UI. We define depth through light and tone.

*   **The Layering Principle:** Stack `surface-container-lowest` on top of `surface-container-low` to create an "offset paper" look. This provides a 3D effect without a single drop shadow.
*   **Ambient Shadows:** Where floating elements (like a "Start Coding" button) require lift, use an ambient shadow:
    *   **Color:** `on-surface` (#191c1e) at 6% opacity.
    *   **Blur:** 40px.
    *   **Y-Offset:** 12px.
    *   This mimics natural light and feels expensive, rather than a generic "drop shadow."
*   **The Ghost Border:** If a form field requires a container, use the `outline_variant` token at **15% opacity**. It should be felt, not seen.

---

## 5. Components: Intentional Primitives

### Buttons (High-Visibility CTAs)
*   **Primary:** `primary` (#005c55) background with `on_primary` (#ffffff) text. 
    *   **Corner Radius:** `xl` (1.5rem/24px) for a pill-shape that feels approachable.
    *   **Padding:** 16px vertical / 32px horizontal.
*   **Secondary:** `surface-container-highest` background. No border.

### Cards & Learning Modules
*   **Style:** `surface-container-lowest` background. 
*   **Radius:** `xl` (1.5rem/24px).
*   **Spacing:** Use "Super-Padding" (at least 40px internal padding) to ensure the content doesn't feel cramped. 
*   **Constraint:** **Strictly no divider lines.** Use 24px of vertical white space to separate the header from the card body.

### Input Fields
*   **Style:** `surface-container-high` background to provide a clear "trough" for typing.
*   **Focus State:** A 2px "Ghost Border" using `primary` at 40% opacity. This provides a soft glow indicating the field is active without harsh contrast.

### AI Insight Chips
*   **Style:** `secondary_container` (#c5e6e1) with `on_secondary_container` (#4a6864) text.
*   **Usage:** Small, rounded indicators for "AI-Powered" tips or "Expert Level" tags.

---

## 6. Do's and Don'ts

### Do:
*   **Do** use asymmetrical layouts (e.g., a large headline on the left with 40% empty space on the right) to create a premium editorial feel.
*   **Do** use the `primary_container` (#0f766e) for deep-set backgrounds where high-contrast white text will sit.
*   **Do** ensure all interactive targets (buttons, links) have at least 48px of "hit area" to accommodate various levels of motor dexterity.

### Don't:
*   **Don't** use pure black (#000000). Always use `on_surface` (#191c1e) for text to reduce eye strain.
*   **Don't** use "Standard" 4px or 8px corners. For this demographic, we use `xl` (1.5rem) or `lg` (1rem) to ensure the UI feels soft and non-threatening.
*   **Don't** use decorative icons. Every icon must serve a functional purpose (e.g., an arrow indicating a path forward).
*   **Don't** use dividers or horizontal rules. Rely on the **Tonal Layering** of different surface colors to separate content sections.