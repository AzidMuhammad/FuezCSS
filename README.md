<div align="center">

<br/>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./logo.png">
  <source media="(prefers-color-scheme: light)" srcset="./logo.png">
  <img src="./logo.png" alt="FuezCSS Logo" width="90" height="90" />
</picture>

<br/><br/>

<h2>FuezCSS</h2>

<p>Utility-first CSS framework, powered by PostCSS.<br/>Scan your templates. Generate only what you use. Ship clean CSS.</p>

<br/>

[![npm](https://img.shields.io/npm/v/fuezcss?style=flat-square&color=000&labelColor=000&logo=npm&logoColor=fff)](https://www.npmjs.com/package/fuezcss)
[![downloads](https://img.shields.io/npm/dm/fuezcss?style=flat-square&color=000&labelColor=000)](https://www.npmjs.com/package/fuezcss)
[![license](https://img.shields.io/npm/l/fuezcss?style=flat-square&color=000&labelColor=000)](./LICENSE)
[![docs](https://img.shields.io/badge/docs-online-000?style=flat-square&labelColor=000)](https://fuezcss.netlify.app)

<br/>

**[Documentation](https://fuezcss.netlify.app)** · **[Playground](https://fuezcss.netlify.app/playground)** · **[Changelog](./CHANGELOG.md)**

<br/>

</div>

---

## What is FuezCSS?

FuezCSS scans your HTML files, JavaScript components, and templates for class names — then generates **only** the CSS you actually reference. The result is a single, static `.css` file with no unused rules and no JavaScript runtime.

It works as a PostCSS plugin, so it drops into any existing pipeline with one line of config.

```css
/* src/assets/index.css */
@fuezcss base;
@fuezcss layout;
@fuezcss utilities;
```

```bash
npx postcss src/assets/index.css -o src/assets/fuez.css
```

---

## Install

```bash
npm install fuezcss postcss postcss-cli autoprefixer
npx fuezcss init
```

`fuezcss init` scaffolds both `postcss.config.js` and `fuez.config.js` automatically.

---

## Quick Start

### 1. Configure PostCSS

```js
// postcss.config.js
module.exports = {
  plugins: [
    require('fuezcss'),
    require('autoprefixer'),
  ],
}
```

### 2. Configure your theme

```js
// fuez.config.js
module.exports = {
  theme: {
    extend: {},
  },
  plugins: [],
}
```

### 3. Add directives

```css
/* src/assets/index.css */
@fuezcss base;       /* reset + base styles     */
@fuezcss layout;     /* grid, navbar, containers */
@fuezcss utilities;  /* colors, type, spacing    */
```

### 4. Build

```bash
npx postcss src/assets/index.css -o src/assets/fuez.css
```

### 5. Import and use

```html
<!doctype html>
<html>
  <head>
    <link href="/src/assets/fuez.css" rel="stylesheet" />
  </head>
  <body class="bg-modern-black">

    <div class="navbar clear nav-top">
      <div class="row content">
        <a href="#">
          <img class="logo" src="/assets/logo.png" />
        </a>
      </div>
    </div>

    <h1 class="text-base font-strong font-modern-white">
      Hello world!
    </h1>

  </body>
</html>
```

---

## Utility Reference

### Layout

| Class | Description |
|---|---|
| `navbar` | Horizontal navigation bar |
| `nav-top` | Pins navbar to top of viewport |
| `clear` | Clears floated children |
| `row` | Flex row container |
| `content` | Centered content wrapper with max-width |

### Colors

| Class | Description |
|---|---|
| `bg-modern-black` | Background — deep black `#0a0a0a` |
| `bg-modern-white` | Background — clean white `#ffffff` |
| `font-modern-black` | Text — deep black |
| `font-modern-white` | Text — clean white |

### Typography

| Class | Property | Value |
|---|---|---|
| `text-sm` | `font-size` | `0.875rem` |
| `text-base` | `font-size` | `1rem` |
| `text-lg` | `font-size` | `1.125rem` |
| `text-xl` | `font-size` | `1.25rem` |
| `font-light` | `font-weight` | `300` |
| `font-normal` | `font-weight` | `400` |
| `font-strong` | `font-weight` | `700` |

### Spacing

Scale: `1` = `0.25rem`, `2` = `0.5rem`, `4` = `1rem`, `8` = `2rem`

| Class | Property |
|---|---|
| `p-{n}` | Padding — all sides |
| `px-{n}` | Padding — horizontal |
| `py-{n}` | Padding — vertical |
| `m-{n}` | Margin — all sides |
| `mx-{n}` | Margin — horizontal |
| `my-{n}` | Margin — vertical |

> Full reference → **[fuezcss.netlify.app/docs](https://fuezcss.netlify.app/docs)**

---

## Framework Integration

<details>
<summary>Vite</summary>

```js
// vite.config.js
import { defineConfig } from 'vite'

export default defineConfig({
  css: {
    postcss: './postcss.config.js',
  },
})
```

</details>

<details>
<summary>Next.js</summary>

```js
// postcss.config.js
module.exports = {
  plugins: {
    fuezcss: {},
    autoprefixer: {},
  },
}
```

```js
// pages/_app.js
import '../styles/fuez.css'
```

</details>

<details>
<summary>Vue 3 / Nuxt</summary>

```js
// postcss.config.cjs
module.exports = {
  plugins: {
    fuezcss: {},
    autoprefixer: {},
  },
}
```

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  postcss: {
    plugins: { fuezcss: {} },
  },
})
```

</details>

<details>
<summary>SvelteKit</summary>

```js
// postcss.config.js
module.exports = {
  plugins: [require('fuezcss'), require('autoprefixer')],
}
```

</details>

---

## Extending the Theme

```js
// fuez.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand:       '#6C47FF',
        'brand-light': '#A78BFA',
        'brand-dark':  '#4C2DB3',
      },
      fontFamily: {
        sans:    ['Inter', 'sans-serif'],
        display: ['Cal Sans', 'Inter', 'sans-serif'],
      },
      spacing: {
        18: '4.5rem',
        72: '18rem',
        96: '24rem',
      },
    },
  },
}
```

---

## Project Structure

```
your-project/
├── src/
│   └── assets/
│       ├── index.css       ← @fuezcss directives (source)
│       └── fuez.css        ← generated output   (add to .gitignore)
├── fuez.config.js
├── postcss.config.js
└── package.json
```

Add the output file to `.gitignore` — it's a build artifact:

```
# .gitignore
src/assets/fuez.css
```

---

## Contributing

Contributions are welcome — new utilities, bug fixes, documentation, framework guides.

```bash
git clone https://github.com/AzidMuhammad/fuezcss.git
cd fuezcss
npm install
npm run build
npm test
```

Open an issue before submitting a large pull request so we can align on direction first.

---

## License

[MIT](./LICENSE) © [Azid Muhammad](https://github.com/AzidMuhammad)

---

<div align="center">
<sub>Made with care by <a href="https://github.com/AzidMuhammad">Azid Muhammad</a></sub>
</div>
