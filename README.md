# 🩺 MedLink VA — Virtual Medical Assistant Services

> A modern, responsive landing page for **MedLink VA**, a virtual medical assistant service offering administrative and clinical support to healthcare professionals worldwide.

---

## 🌐 Live Demo

<!-- Replace with your actual GitHub Pages or deployment URL -->
> [View Live Site](https://yourusername.github.io/medlinkva)

---

## 📋 Overview

MedLink VA is a single-page HTML landing page designed to attract and convert healthcare professionals looking for remote virtual assistant support. The page highlights services, pricing, and contact information — with a lead capture modal and countdown offer timer.

---

## ✨ Features

- **Fully Responsive** — Mobile, tablet, and desktop friendly
- **Lead Capture Modal** — Auto-opens after 7 seconds with a consultation booking form
- **Countdown Timer** — 48-hour urgency timer (persists across page refreshes via `localStorage`)
- **Scroll Reveal Animations** — Elements animate in as the user scrolls
- **Mailto Integration** — Forms open the user's email client pre-filled with their details, addressed to `medlinkva@gmail.com`
- **Mobile Navigation** — Hamburger menu for smaller screens
- **Glassmorphism UI** — Deep navy/teal design with glass-card components
- **No Dependencies / No Build Step** — Pure HTML, CSS, and vanilla JavaScript

---

## 🗂️ Project Structure

```
medlinkva/
│
├── index.html        # Main landing page (single file — all HTML, CSS & JS)
└── README.md         # Project documentation
```

---

## 🚀 Getting Started

### View Locally

No setup required. Simply clone and open in your browser:

```bash
git clone https://github.com/yourusername/medlinkva.git
cd medlinkva
open index.html
```

### Deploy to GitHub Pages

1. Push the repository to GitHub
2. Go to **Settings → Pages**
3. Under **Source**, select `main` branch and `/ (root)`
4. Click **Save** — your site will be live at `https://yourusername.github.io/medlinkva`

---

## 📬 Contact Form Behaviour

Both the popup modal form and the inline contact form use a `mailto:` link to send enquiries. When submitted, the user's default email client opens with a pre-filled message to:

```
medlinkva@gmail.com
```

> **Note:** No backend or email API is required. For automated form delivery, consider integrating [Formspree](https://formspree.io) or [EmailJS](https://www.emailjs.com).

---

## 🎨 Design Highlights

| Element | Detail |
|---|---|
| **Fonts** | Playfair Display (headings), DM Sans (body) via Google Fonts |
| **Colour Palette** | Navy `#0a1628`, Teal `#0097a7`, Sky Blue `#4fc3f7` |
| **Animations** | CSS keyframes + IntersectionObserver scroll reveal |
| **Layout** | CSS Grid & Flexbox — no frameworks |

---

## 📦 Tech Stack

- **HTML5**
- **CSS3** (custom properties, grid, flexbox, animations)
- **Vanilla JavaScript** (no libraries or frameworks)
- **Google Fonts**

---

## 📄 Sections

1. **Urgency Banner** — Countdown offer strip at the top
2. **Navigation** — Fixed nav with smooth-scroll links and CTA
3. **Hero** — Headline, subtext, animated orb visual, and floating cards
4. **Stats Bar** — Key metrics at a glance
5. **Services** — Administrative and EHR/Clinical support cards
6. **Why Us** — Differentiators and trust badges
7. **Pricing** — Single all-inclusive plan with urgency countdown
8. **Contact** — Contact details and inline message form
9. **Footer** — Brand summary and contact info
10. **Modal Popup** — Consultation booking form

---

## 🛠️ Customisation

| What to change | Where to find it |
|---|---|
| Business email | Search `medlinkva@gmail.com` — replace all instances |
| Phone number | Search `+256 785 724 420` |
| Pricing | Find `.price-new` and `.price-old` values |
| Offer duration | Change `48*3600*1000` in the countdown script |
| Brand name | Search `MedLink VA` |
| Colours | Edit CSS variables in `:root` at the top of `<style>` |

---

## 📃 License

This project is for personal/commercial use by MedLink VA. Feel free to adapt for your own business.

---

> Built with ❤️ for healthcare professionals who deserve more time with their patients.
