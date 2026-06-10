<div align="center">

<br />

<img src="https://fuezcss.netlify.app/logo.png" alt="FuezCSS" width="72" height="72" />

<h1>FuezCSS</h1>

<p>
  A lightweight, utility-first CSS framework powered by PostCSS.<br />
  Scan. Generate. Ship — only the CSS you actually use.
</p>

<p>
  <a href="https://www.npmjs.com/package/fuezcss"><img src="https://img.shields.io/npm/v/fuezcss?style=flat-square&colorA=18181B&colorB=6C47FF" alt="npm version" /></a>
  <a href="https://www.npmjs.com/package/fuezcss"><img src="https://img.shields.io/npm/dm/fuezcss?style=flat-square&colorA=18181B&colorB=6C47FF" alt="monthly downloads" /></a>
  <a href="https://github.com/AzidMuhammad/fuezcss/blob/main/LICENSE"><img src="https://img.shields.io/npm/l/fuezcss?style=flat-square&colorA=18181B&colorB=6C47FF" alt="license" /></a>
  <a href="https://fuezcss.netlify.app"><img src="https://img.shields.io/badge/docs-fuezcss.netlify.app-6C47FF?style=flat-square&colorA=18181B" alt="documentation" /></a>
</p>

<p>
  <a href="https://fuezcss.netlify.app">Documentation</a> ·
  <a href="https://fuezcss.netlify.app/playground">Playground</a> ·
  <a href="https://github.com/AzidMuhammad/fuezcss/issues">Report a Bug</a> ·
  <a href="https://github.com/AzidMuhammad/fuezcss/discussions">Discussions</a>
</p>

<br />

</div>

---

## Overview

FuezCSS scans all of your HTML files, JavaScript components, and templates for class names, generates the corresponding styles, and writes them to a single static CSS file. Only the classes you use make it into your bundle — nothing else.

```html
<body class="bg-modern-black">
  <h1 class="text-base font-strong font-modern-white">
    Hello world!
  </h1>
</body>
```

No runtime overhead. No unused styles. Just clean, production-ready CSS.

---

## Features

- **Utility-first** — compose styles directly in your markup, no custom CSS required
- **Scan-based** — generates only the classes referenced in your source files
- **PostCSS-native** — integrates into any existing PostCSS pipeline in seconds
- **Configurable theme** — extend colors, typography, and spacing in `fuez.config.js`
- **Plugin architecture** — add your own utilities, components, and directives
- **Zero JS runtime** — the output is a plain, static `.css` file

---

## Getting Started

### Installation

```bash
npm install fuezcss postcss postcss-cli autoprefixer
```

### Initialize

```bash
npx fuezcss init
```

This creates `postcss.config.js` and `fuez.config.js` in your project root.

---

## Configuration

### `postcss.config.js`

```js
module.exports = {
  plugins: [
    require('fuezcss'),
    require('autoprefixer')
  ]
}
```

### `fuez.config.js`

```js
module.exports = {
  theme: {
    extend: {
      // Override or extend default tokens here
    }
  },
  plugins: []
}
```

---

## Usage

### 1 — Add directives to your entry CSS

Create `src/assets/index.css`:

```css
@fuezcss base;
@fuezcss layout;
@fuezcss utilities;
```

### 2 — Build

```bash
npx postcss src/assets/index.css -o src/assets/fuez.css
```

### 3 — Import in your HTML

```html
<!doctype html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link href="/src/assets/fuez.css" rel="stylesheet" />
  </head>
  <body class="bg-modern-black">
    <h1 class="text-base font-strong font-modern-white">Hello world!</h1>
  </body>
</html>
```

### 4 — Run your project

```bash
npm run dev
```

---

## Utility Reference

### Colors

| Class | Value | Usage |
|---|---|---|
| `bg-modern-black` | `#0a0a0a` | Background |
| `bg-modern-white` | `#ffffff` | Background |
| `font-modern-black` | `#0a0a0a` | Text color |
| `font-modern-white` | `#ffffff` | Text color |

### Typography

| Class | Property | Value |
|---|---|---|
| `text-sm` | `font-size` | `0.875rem` |
| `text-base` | `font-size` | `1rem` |
| `text-lg` | `font-size` | `1.125rem` |
| `text-xl` | `font-size` | `1.25rem` |
| `text-2xl` | `font-size` | `1.5rem` |
| `font-light` | `font-weight` | `300` |
| `font-normal` | `font-weight` | `400` |
| `font-strong` | `font-weight` | `700` |

### Layout

| Class | Property |
|---|---|
| `flex` | `display: flex` |
| `grid` | `display: grid` |
| `block` | `display: block` |
| `inline` | `display: inline` |
| `hidden` | `display: none` |

### Spacing

FuezCSS uses a base-4 scale (`p-1` = `0.25rem`, `p-2` = `0.5rem`, etc.):

| Class | Shorthand |
|---|---|
| `p-{n}` | `padding` all sides |
| `px-{n}` | `padding-left` + `padding-right` |
| `py-{n}` | `padding-top` + `padding-bottom` |
| `m-{n}` | `margin` all sides |
| `mx-{n}` | `margin-left` + `margin-right` |
| `my-{n}` | `margin-top` + `margin-bottom` |

> Full reference at **[fuezcss.netlify.app](https://fuezcss.netlify.app)**

---

## Framework Integration

<details>
<summary><strong>Vite</strong></summary>

```js
// vite.config.js
import { defineConfig } from 'vite'

export default defineConfig({
  css: {
    postcss: './postcss.config.js'
  }
})
```

</details>

<details>
<summary><strong>Next.js</strong></summary>

```js
// postcss.config.js
module.exports = {
  plugins: {
    fuezcss: {},
    autoprefixer: {}
  }
}
```

Then import the built file in `_app.js`:

```js
import '../styles/fuez.css'
```

</details>

<details>
<summary><strong>Vue 3 / Nuxt</strong></summary>

```js
// postcss.config.cjs
module.exports = {
  plugins: {
    fuezcss: {},
    autoprefixer: {}
  }
}
```

```js
// nuxt.config.ts
export default defineNuxtConfig({
  postcss: {
    plugins: {
      fuezcss: {}
    }
  }
})
```

</details>

<details>
<summary><strong>React / Create React App</strong></summary>

```js
// postcss.config.js
module.exports = {
  plugins: [
    require('fuezcss'),
    require('autoprefixer')
  ]
}
```

</details>

---

## Extending the Theme

Add custom tokens in `fuez.config.js` under `theme.extend`:

```js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand:       '#6C47FF',
        'brand-50':  '#EDE9FF',
        'brand-900': '#1E0A7A',
      },
      fontFamily: {
        sans:    ['Inter', 'sans-serif'],
        display: ['Cal Sans', 'Inter', 'sans-serif'],
      },
      spacing: {
        18: '4.5rem',
        72: '18rem',
      }
    }
  }
}
```

---

## Project Structure

```
your-project/
├── src/
│   └── assets/
│       ├── index.css       ← @fuezcss directives
│       └── fuez.css        ← generated output (gitignore this)
├── fuez.config.js           ← theme & plugin config
├── postcss.config.js        ← PostCSS pipeline
└── package.json
```

> **Tip:** Add `src/assets/fuez.css` to your `.gitignore` — it's a build artifact, not source code.

---

## Contributing

All contributions are welcome — bug fixes, new utilities, documentation improvements, or framework integrations.

```bash
# Clone the repo
git clone https://github.com/AzidMuhammad/fuezcss.git
cd fuezcss

# Install dependencies
npm install

# Run tests
npm test

# Build
npm run build
```

Please open an issue before submitting a large PR so we can discuss the direction first.

---

## License

MIT — see [LICENSE](./LICENSE) for details.

---

<div align="center">

<sub>Built with ❤️ by <a href="https://github.com/AzidMuhammad">Azid Muhammad</a></sub>

</div>
