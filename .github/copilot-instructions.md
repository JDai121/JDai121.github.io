<!--
Purpose: Give AI coding agents concise, repo-specific guidance so they
can be productive immediately. Keep changes small and factual — do not
invent unobserved workflows.
-->
# Copilot / AI Agent Instructions

Summary
- This repository is a minimal static site: a single `index.html` that
  mounts a small React app using CDN-served React, ReactDOM and
  `@babel/standalone` to enable in-browser JSX (`type="text/babel"`).

Big picture
- Single-page static site (no build system): see [index.html](index.html).
- Runtime: browser loads React + Babel from unpkg CDNs and executes JSX
  at runtime. There are no local JS modules, bundlers, or test runners in
  the repo.

What to watch for (project-specific patterns)
- `index.html` includes these external scripts:
  - `https://unpkg.com/react@18/umd/react.development.js`
  - `https://unpkg.com/react-dom@18/umd/react-dom.development.js`
  - `https://unpkg.com/@babel/standalone/babel.min.js`
  Any change that affects component syntax needs to keep JSX transpiled
  for the browser (or move code into a prebuilt bundle).
- In-file JSX: components are defined inside a `<script type="text/babel">`.
  If you extract JS to new files, remember the environment is currently
  unbundled and served directly to the browser.
- DOM mount and render pattern (example from repo):
  ```js
  const domNode = document.getElementById('app')
  const root = ReactDOM.createRoot(domNode)
  root.render(<h1> <MainBody /> </h1>)
  ```
  Note: `MainBody` already renders headings; avoid creating invalid
  nested `<h1>` elements when refactoring.

Developer workflows (how to run & debug)
- Quick local preview (PowerShell):
  ```powershell
  cd <repo-root>
  python -m http.server 8000
  Start-Process http://localhost:8000
  ```
- Alternative: use the VS Code "Live Server" extension or `npx http-server`.
- There are no tests or build steps to run from repo files. If you add
  a bundler or test framework, include clear README updates.

Integration & dependencies
- Project relies entirely on CDN-hosted JS — changing external URLs or
  upgrading major versions (React 18 -> 19) must be tested in-browser.
- No server-side integrations or CI config found in the repository.

What to change when expanding the project
- Prefer moving larger components into separate `.js` files and then
  either keep using `type="text/babel"` or introduce a build step
  (e.g., Vite/webpack) and update documentation accordingly.
- When adding new files, update this instruction file with any new
  developer commands (test/build/serve) and add a brief example.

If anything is ambiguous or you need additional details (deploy targets,
CI, or intended GitHub Pages settings), ask the repo owner for those
details so these instructions can be updated.

---
Do you want me to (pick one):
- add a simple local `serve` script and README snippet, or
- scaffold a basic `package.json` + npm-based dev server?
