# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

Project overview
- This is a static site with interactive portfolio management.
- Core files: index.html, src/styles/main.css, src/js/main.js.
- JavaScript uses ES6 modules and modern browser features (localStorage, CSS custom properties).
- UI state & user portfolios persisted in localStorage.

Common commands
- Install dependencies and run a modern dev server (preferred):
  ```bash
  npm install
  npm run dev         # Vite dev server (auto-reloads)
  npm run build       # Production build to dist/
  npm run preview     # Preview the build
  ```

- Legacy simple server (still works):
  ```bash
  python3 -m http.server 8000
  ```

- Code quality:
  ```bash
  npm run lint          # Find lint issues
  npm run lint:fix       #Fix many issues
  npm run format         # Format with Prettier
  npm run format:check   # Check formatting
  ```

- Direct browser open (no server):
  ```bash
  open index.html
  ```

Linting, formatting, tests
- ESLint configured for modern browser ES2022 with semicolons and single quotes.
- Prettier configured for 80 chars, LF line endings, 2-space indent.
- No test framework configured yet.

Code architecture (big picture)
- HTML: index.html uses semantic markup (header, main, footer, modal dialogs).
  - Portfolio list region with search input and category filter buttons.
  - Controls for theme toggle (dark/light) and "New Portfolio" modal trigger.
  - Two modals: one for viewing portfolios, one for creating portfolios.

- CSS: CSS custom properties (:root) for theming (light vs dark).
  - Responsive design with flexbox/grid and mobile-first media queries.
  - Component styles: search/filter controls, portfolio cards, modals, forms.
  - Dark theme toggles colors via body.dark-theme class.

- JS: src/js/main.js is fully modular.
  - Theme init: reads/persists user preference, controls aria-pressed on toggle button.
  - Search/filter: live UI updates, persists last query/filter to localStorage.
  - Modals: generic open/close with overlay click and Escape keys.
  - Document creation: handles form submission, stores in localStorage, renders new cards.
  - Persistence: last query/filter and created documents survive page reload.

- Data storage:
  - myFolio:lastQuery + myFolio:lastFilter keys for search/filter state.
  - myFolio:docs object array holds user portfolios (id, title, category, summary).

Development tips for this repo
- You can edit without rebuild; changes appear on refresh or automatically via Vite dev server.
- All styling is in main.css for simplicity; add styles there or create modular CSS imports.
- To create a new static page, copy index.html and adjust markup; keep script/style links.
- The repo now supports import/export and other ES6+ features thanks to Vite build.

Repository conventions
- npm scripts for dev, lint, format, build, preview.
- .eslintrc.json and .prettierrc.json enforce consistent code style.
- New files go under src/ by type (js/, styles/) unless they’re a full page (index.html).
- No environment variables; everything lives in the browser via localStorage.

What’s missing/future work
- Unit test framework (could be added easily via npm).
- CI/CD pipeline definitions.
- More sophisticated document editing capabilities.

Tools (Step 5)
- Vite for fast dev server and modern bundling.
- ESLint for linting.
- Prettier for formatting.
- Built to run with node 18+ but dev server works in any modern browser.
