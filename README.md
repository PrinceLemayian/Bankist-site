# 🏦 Bankist - When Banking Meets Minimalist

> A sleek, modern bank marketing website built with vanilla JavaScript, demonstrating advanced DOM manipulation, scroll-based effects, and the Intersection Observer API.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Prettier](https://img.shields.io/badge/Code%20Style-Prettier-ff69b4?style=flat-square)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Live Demo](#live-demo)
- [Features](#features)
- [JavaScript Concepts Demonstrated](#javascript-concepts-demonstrated)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Sections Breakdown](#sections-breakdown)
- [Code Highlights](#code-highlights)
- [Course Context](#course-context)
- [Credits](#credits)

---

## Overview

Bankist Site is the **marketing/landing page** for a fictional minimalist bank. It is part of a two-project series from Jonas Schmedtmann's _The Complete JavaScript Course_. This landing page showcases polished, production-style front-end techniques using **zero frameworks or libraries** just HTML, CSS, and modern vanilla JavaScript.

The project places a heavy emphasis on performance patterns (lazy loading, deferred script execution) and progressive enhancement using the **Intersection Observer API** for scroll-driven effects.

---

## Live Demo

> 🚀 _Live Site Demo:_

```
https://princelemayian.github.io/Bankist-site/
```

---

## Features

### UI & Navigation

- **Smooth scroll** to sections via a "Learn more" CTA button
- **Sticky navigation bar** that appears only when the hero section scrolls out of view (powered by Intersection Observer - no `scroll` event listener)
- **Navigation link hover fade effect** using event delegation on the parent `<nav>` element
- **"Open account" modal** accessible from both the nav bar and the sign-up section CTA, with overlay and keyboard (`Escape`) dismissal

### Sections & Components

- **Features section** — Three-column grid showcasing the bank's key selling points with SVG icons and lazy-loaded imagery
- **Operations tabbed component** — Three interactive tabs (Instant Transfers, Instant Loans, Instant Closing) with smooth content switching
- **Testimonials slider** — A fully custom-built image/text carousel with left/right button controls and dot indicators; supports both button clicks and dot navigation
- **Section reveal animations** — Each section fades in from below as it enters the viewport, using Intersection Observer

### Performance

- **Lazy image loading** — Feature section images initially load low-resolution blurred placeholders; the full-resolution versions swap in and the blur lifts only when the image scrolls into view
- **Deferred script loading** — `<script defer>` ensures the JS file is fetched in parallel with HTML parsing but only executes after the DOM is fully ready, with no render blocking

---

## JavaScript Concepts Demonstrated

This project is a practical showcase of the following JavaScript and Web API concepts:

| Concept                                       | Where Used                                              |
| --------------------------------------------- | ------------------------------------------------------- |
| `document.querySelector` / `querySelectorAll` | Selecting all interactive elements                      |
| Event delegation                              | Nav hover fade, tab switching                           |
| Smooth scrolling (`scrollIntoView`)           | "Learn more" CTA button                                 |
| Intersection Observer API                     | Sticky nav, section reveal, lazy loading                |
| DOM class manipulation (`classList`)          | Modal, tabs, slider dots, section visibility            |
| Higher-order functions (`forEach`, `bind`)    | Nav fade handler, dot generation                        |
| Closures                                      | Slider component encapsulation                          |
| Optional data attributes (`data-*`)           | Tab switching (`data-tab`), lazy image src (`data-src`) |
| Modal / overlay pattern                       | "Open account" form                                     |
| Custom slider logic                           | Testimonials carousel with `transform: translateX`      |
| `defer` script attribute                      | Performance-optimized script loading                    |

---

## Project Structure

```
Bankist-site/
│
├── index.html          # Main HTML — structure and content for all sections
├── script.js           # All JavaScript — interactivity and DOM behaviour
├── style.css           # All styling — layout, animations, responsive design
├── .prettierrc         # Prettier config for consistent code formatting
├── README.md           # Project README file
│
└── img/
    ├── logo.png            # Bankist nav logo
    ├── icon.png            # Favicon / footer icon
    ├── hero.png            # Hero section illustration
    ├── icons.svg           # SVG sprite for feature/operation icons
    ├── digital.jpg         # Feature image — full resolution
    ├── digital-lazy.jpg    # Feature image — low-res placeholder
    ├── grow.jpg            # Feature image — full resolution
    ├── grow-lazy.jpg       # Feature image — low-res placeholder
    ├── card.jpg            # Feature image — full resolution
    ├── card-lazy.jpg       # Feature image — low-res placeholder
    ├── user-1.jpg          # Testimonial avatar
    ├── user-2.jpg          # Testimonial avatar
    └── user-3.jpg          # Testimonial avatar
```

---

## Getting Started

No build tools, package managers, or dependencies required. This is a pure HTML/CSS/JS project.

### Run locally

1. **Clone the repository**

   ```bash
   git clone https://github.com/PrinceLemayian/Bankist-site.git
   cd Bankist-site
   ```

2. **Open in your browser**

   Simply open `index.html` directly in any modern browser:

   ```bash
   # macOS
   open index.html

   # Linux
   xdg-open index.html

   # Windows
   start index.html
   ```

   Or use a local dev server for a better experience:

   ```bash
   # With VS Code Live Server extension
   # Right-click index.html → "Open with Live Server"

   # With Node.js http-server
   npx http-server .
   ```

### Browser support

Works in all modern browsers (Chrome, Firefox, Edge, Safari). Intersection Observer API requires a browser that supports it — all evergreen browsers do.

---

## Sections Breakdown

### Header / Hero

- Full-viewport hero with the tagline _"When banking meets minimalist"_
- CTA button smoothly scrolls to the Features section

### Section 1 — Features

Three highlighted features of the fictional bank:

- 100% Digital Bank
- Watch Your Money Grow
- Free Debit Card Included

Each feature card is paired with a lazy-loaded image that reveals in full quality on scroll.

### Section 2 — Operations

An interactive tabbed component with three operational highlights:

- **Tab 1** — Instant Transfers (no fees)
- **Tab 2** — Instant Loans (home purchases, big goals)
- **Tab 3** — Instant Closing (hassle-free account closure)

### Section 3 — Testimonials

A custom-built slider featuring three customer testimonials. Navigation is available via arrow buttons and clickable dot indicators.

### Sign-Up CTA

A high-contrast section with a single CTA button that triggers the "Open account" modal.

### Footer

Standard footer with navigation links and the Bankist logo.

### Modal — Open Account

A centred modal form with First Name, Last Name, and Email fields. Closes on the `×` button, overlay click, or `Escape` key.

---

## Code Highlights

### Intersection Observer for Sticky Nav

```javascript
const stickyNav = function (entries) {
  const [entry] = entries;
  if (!entry.isIntersecting) nav.classList.add('sticky');
  else nav.classList.remove('sticky');
};

const headerObserver = new IntersectionObserver(stickyNav, {
  root: null,
  threshold: 0,
  rootMargin: `-${navHeight}px`,
});

headerObserver.observe(header);
```

### Event Delegation for Nav Hover Fade

```javascript
const handleHover = function (e) {
  if (e.target.classList.contains('nav__link')) {
    const link = e.target;
    const siblings = link.closest('.nav').querySelectorAll('.nav__link');
    siblings.forEach(el => {
      if (el !== link) el.style.opacity = this;
    });
  }
};

nav.addEventListener('mouseover', handleHover.bind(0.5));
nav.addEventListener('mouseout', handleHover.bind(1));
```

### Lazy Image Loading

```javascript
const loadImg = function (entries, observer) {
  const [entry] = entries;
  if (!entry.isIntersecting) return;

  entry.target.src = entry.target.dataset.src;
  entry.target.addEventListener('load', function () {
    entry.target.classList.remove('lazy-img');
  });
  observer.unobserve(entry.target);
};
```

---

## Course Context

This project was built while working through **[The Complete JavaScript Course: From Zero to Expert!](https://www.udemy.com/course/the-complete-javascript-course/)** by Jonas Schmedtmann (Sections 13–14 — Advanced DOM and Events).

**What this project taught:**

- How to build real interactive UI without relying on jQuery or any framework
- Performance-aware JavaScript — using Intersection Observer instead of costly scroll listeners
- Thinking in terms of event delegation rather than attaching listeners to every element individually
- Structuring a clean, readable vanilla JS codebase

---

## Credits

- **Developer:** [Lemayian](https://github.com/PrinceLemayian)
- **Original course design:** [Jonas Schmedtmann](https://github.com/jonasschmedtmann) — _The Complete JavaScript Course_
