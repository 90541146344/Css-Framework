
# AuroraCSS — Custom Sass-based CSS Framework

> **Project:** Custom CSS Framework (Sass)
>
> **Team size:** 3–4 students  
> **Deliverables:** Sass source (partials), compiled CSS (`dist/aurora.css` and `dist/aurora.min.css`), `README.md` (this file), demo HTML (`/docs/index.html`), and a PDF version of this README.

---

## Overview / Objective

Build a custom, reusable CSS framework using **Sass** partials and variables. The framework must:

- Provide a coherent theme for standard HTML elements (headings, lists, buttons, forms, inputs, tables, etc.).
- Include utility classes for common styling (colors, font-weight, font-size, margin, padding, borders).
- Be customizable (using Sass variables or CSS custom properties).
- Include the compiled CSS in the repository.
- Include installation, usage, and customization instructions in the `README.md`.

---

## Quick step‑by‑step (Team + GitHub setup)

1. **Choose a team leader**  
   - Leader creates the public GitHub repository. Suggested repo name: `aurora-css-framework` (replace `aurora` with your framework name).

2. **Create the repo (GitHub UI)**  
   - On GitHub: *New repository* → name it → set **Public** → Initialize with `.gitignore` (Node) optionally → Create repository.

   *Or using GitHub CLI (optional):*
   ```bash
   gh repo create your-org/aurora-css-framework --public --confirm
   ```

3. **Add collaborators**  
   - Settings → Manage access → Invite collaborators (add your teammates' GitHub usernames).

4. **Local setup & first commit**
   ```bash
   git clone git@github.com:<your-org>/aurora-css-framework.git
   cd aurora-css-framework
   npm init -y
   npm install --save-dev sass
   ```

5. **Branching workflow**  
   - Use `main` as protected; development branches for features: `feature/variables`, `feature/utilities`, `feature/components`. Open PRs for reviews.

6. **Deliverables to include in repo**
   - `scss/` (Sass partials)
   - `dist/aurora.css` and `dist/aurora.min.css`
   - `docs/index.html` (demo)
   - `README.md` + `README.pdf`
   - `package.json` scripts for building CSS
   - Optional: screenshots, CHANGELOG, LICENSE

---

## Recommended repository structure

```
aurora-css-framework/
├─ scss/
│  ├─ _variables.scss
│  ├─ _mixins.scss
│  ├─ _base.scss
│  ├─ _components.scss
│  ├─ _utilities.scss
│  └─ main.scss
├─ dist/
│  ├─ aurora.css
│  └─ aurora.min.css
├─ docs/
│  └─ index.html
├─ package.json
├─ README.md
└─ README.pdf
```

---

## Sass partials & conventions (what to create)

### `_variables.scss`
- Define design tokens as Sass variables.
- Expose key tokens as **CSS custom properties** (so end-users can override them at runtime).

Example:
```scss
// _variables.scss
$font-family-sans: "Inter", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
$font-size-base: 16px;

$color-primary: #0d6efd;
$color-secondary: #6c757d;
$color-success: #198754;
$color-danger: #dc3545;
$color-muted: #6c757d;
$bg-default: #ffffff;
$text-default: #212529;

/* Export to CSS custom properties so users can override in plain CSS */
:root {
  --font-family-sans: #{$font-family-sans};
  --font-size-base: #{$font-size-base};
  --color-primary: #{$color-primary};
  --color-secondary: #{$color-secondary};
  --color-success: #{$color-success};
  --color-danger: #{$color-danger};
  --bg-default: #{$bg-default};
  --text-default: #{$text-default};
}
```

### `_mixins.scss`
- Reusable mixins (center, visually-hidden, button reset).

Example:
```scss
@mixin visually-hidden {
  position: absolute !important;
  height: 1px; width: 1px;
  overflow: hidden; clip: rect(1px, 1px, 1px, 1px);
  white-space: nowrap;
}
```

### `_base.scss`
- Normalize/Reset (minimal)
- Typography rules (h1..h6), body, lists, links.

Example:
```scss
body {
  font-family: var(--font-family-sans);
  font-size: var(--font-size-base);
  color: var(--text-default);
  background-color: var(--bg-default);
  line-height: 1.6;
  margin: 0;
  padding: 0;
}

h1, h2, h3, h4, h5, h6 {
  margin: 0 0 0.5rem 0;
  line-height: 1.2;
  color: var(--text-default);
}

a { color: var(--color-primary); text-decoration: none; }
a:hover { text-decoration: underline; }
```

### `_components.scss`
- Buttons, cards, forms, inputs, tables.

Button example:
```scss
.btn {
  display: inline-block;
  padding: 0.5rem 0.875rem;
  border-radius: 6px;
  border: 1px solid transparent;
  background: var(--color-primary);
  color: #fff;
  font-weight: 600;
  text-align: center;
  cursor: pointer;
  transition: background .15s ease, transform .05s;
}

.btn--secondary { background: var(--color-secondary); color: #fff; }
.btn--outline {
  background: transparent;
  border-color: var(--color-primary);
  color: var(--color-primary);
}
```

### `_utilities.scss`
- Small, single‑purpose classes. Use Sass loops to generate spacing utilities and sizes.

Example (spacing utilities):
```scss
// generate .m-{n} and .p-{n}
$space-scale: (0: 0, 1: .25rem, 2: .5rem, 3: 1rem, 4: 1.5rem, 5: 3rem);
@each $k, $v in $space-scale {
  .m-#{$k} { margin: $v !important; }
  .mt-#{$k} { margin-top: $v !important; }
  .mb-#{$k} { margin-bottom: $v !important; }
  .p-#{$k} { padding: $v !important; }
  .pt-#{$k} { padding-top: $v !important; }
  .pb-#{$k} { padding-bottom: $v !important; }
}
```

---

## main.scss (imports)
```scss
@import 'variables';
@import 'mixins';
@import 'base';
@import 'components';
@import 'utilities';
```

---

## Enabling runtime customization for users

Because compiled Sass variables are static at build-time, expose the main tokens as CSS variables (see `_variables.scss` above). Users may override them by adding a small CSS file after your framework:

```css
/* custom.css (loaded AFTER aurora.css) */
:root {
  --color-primary: #ff6b6b;
  --font-size-base: 18px;
}
```

Or include a `custom.css` in `docs/index.html` to let instructors or clients tweak the theme.

---

## Build / Development commands

Install:
```bash
npm install
# sass is a dev dependency (see package.json that you add)
```

Suggested `package.json` scripts:
```json
"scripts": {
  "build:css": "sass scss:dist --no-source-map",
  "build:css:prod": "sass scss:dist --style=compressed --no-source-map",
  "watch:css": "sass --watch scss:dist --no-source-map"
}
```

- `npm run build:css` → compiles readable `dist/aurora.css`
- `npm run build:css:prod` → compiles minified `dist/aurora.min.css`
- `npm run watch:css` → watches `scss/` and recompiles on change

---

## Usage (example `docs/index.html`)

```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>AuroraCSS demo</title>
  <link rel="stylesheet" href="../dist/aurora.css" />
  <!-- Optional custom overrides: -->
  <link rel="stylesheet" href="custom.css" />
</head>
<body>
  <header class="site-header">
    <h1>Welcome to AuroraCSS</h1>
    <p class="lead">Simple demo of theme + utilities</p>
  </header>

  <section>
    <h2>Buttons</h2>
    <button class="btn">Primary</button>
    <button class="btn btn--secondary">Secondary</button>
    <button class="btn btn--outline">Outline</button>
  </section>

  <section>
    <h2>Form</h2>
    <label for="name">Name</label>
    <input id="name" type="text" placeholder="Your name" />
  </section>
</body>
</html>
```

---

## Accessibility & Quality notes

- Ensure focus states for interactive elements (`:focus { outline: 2px solid ... }`).
- Use sufficient color contrast for text and backgrounds.
- Keep utility class names predictable and documented.
- Test the demo page in mobile widths and a screen reader if possible.

---

## What to include in your final submission (assignment checklist)

- [ ] Public GitHub repository (team leader created)
- [ ] `README.md` (this file)
- [ ] `README.pdf` (PDF copy)
- [ ] `scss/` source partials (Sass files)
- [ ] `dist/` compiled CSS (readable + minified)
- [ ] `docs/index.html` demo showing theme + utilities
- [ ] Screenshots (optional) showing responsive behavior
- [ ] `package.json` and build scripts
- [ ] CONTRIBUTING and LICENSE (recommended)

---

## Grading-focused tips (how to maximize marks)

- **Sass partials**: Use multiple partials — variables, mixins, base, components, utilities. Don't keep everything in one file.
- **Variables & customisation**: Export important design tokens as CSS variables for runtime overrides.
- **Utilities**: Implement a compact but useful utility set (spacing, colors, text-size, font-weight).
- **Theme consistency**: Ensure buttons, forms, tables share the same color palette & type scale.
- **Documentation**: README must show installation, usage, how to override variables, and how to build the compiled CSS.
- **Compiled files in repo**: Remember to commit `dist/aurora.css` and `dist/aurora.min.css`.

---

## Example credits / contact

If you need somebody to review your PRs or check your implementation, list each team member with GitHub username in the repo root (e.g., `TEAM.md`).

---

## License

Add a license (e.g., MIT) in `LICENSE` file.

---

Thank you — this `README.md` provides a complete, step-by-step guide and ready-to-paste content. Replace `aurora` with your preferred framework name where needed.
