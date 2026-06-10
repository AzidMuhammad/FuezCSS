# FuezCSS

**A lightweight, utility-first CSS framework powered by PostCSS.**

FuezCSS works by scanning all of your HTML files, JavaScript components, and any other templates for class names, generating the corresponding styles, and writing them to a static CSS file — keeping your final bundle lean and production-ready.

[![npm version](https://img.shields.io/npm/v/fuezcss)](https://www.npmjs.com/package/fuezcss)
[![npm downloads](https://img.shields.io/npm/dm/fuezcss)](https://www.npmjs.com/package/fuezcss)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## ✨ Features

- **Utility-first** — style directly in your markup, no custom CSS needed
- **PostCSS-powered** — integrates seamlessly into any PostCSS pipeline
- **Scan-based purging** — only generates classes you actually use
- **Configurable theme** — extend colors, fonts, spacing, and more via `fuez.config.js`
- **Plugin support** — extend FuezCSS with your own plugins
- **Zero JS runtime** — outputs a plain static CSS file

---

## 📦 Installation

```bash
npm install fuezcss postcss postcss-cli
npx fuezcss init
```

---

## ⚙️ Configuration

After running `npx fuezcss init`, two config files will be created:

### `postcss.config.js`

```js
module.exports = {
  plugins: [
    require('fuezcss'),
    require('autoprefixer')
  ]
};
```

### `fuez.config.js`

```js
module.exports = {
  theme: {
    extend: {
      // Add your custom tokens here
    }
  },
  plugins: [
    // Add your plugins here
  ]
};
```

---

## 🚀 Quick Start

### 1. Add the FuezCSS directives

Create `src/assets/index.css` and add:

```css
@fuezcss base;
@fuezcss layout;
@fuezcss utilities;
```

### 2. Build your CSS

```bash
npx postcss src/assets/index.css -o src/assets/fuez.css
```

### 3. Link it in your HTML

```html
<!doctype html>
<html>
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="/src/assets/fuez.css" rel="stylesheet">
  </head>
  <body class="bg-modern-black">
    <h1 class="text-base font-strong font-modern-white">
      Hello world!
    </h1>
  </body>
</html>
```

### 4. Run your project

```bash
npm run dev
```

---

## 🎨 Utility Classes

### Colors

| Class | Description |
|---|---|
| `bg-modern-black` | Background: deep modern black |
| `bg-modern-white` | Background: clean white |
| `font-modern-black` | Text color: deep modern black |
| `font-modern-white` | Text color: clean white |

### Typography

| Class | Description |
|---|---|
| `text-base` | Base font size |
| `text-sm` | Small font size |
| `text-lg` | Large font size |
| `text-xl` | Extra large font size |
| `font-strong` | Bold font weight |
| `font-light` | Light font weight |

### Layout

| Class | Description |
|---|---|
| `flex` | `display: flex` |
| `grid` | `display: grid` |
| `block` | `display: block` |
| `hidden` | `display: none` |

### Spacing

| Class | Description |
|---|---|
| `p-{n}` | Padding all sides |
| `px-{n}` | Padding horizontal |
| `py-{n}` | Padding vertical |
| `m-{n}` | Margin all sides |
| `mx-{n}` | Margin horizontal |
| `my-{n}` | Margin vertical |

> Full utility reference: [fuezcss.netlify.app](https://fuezcss.netlify.app)

---

## 🛠 Framework Integration

### Vite

```js
// vite.config.js
import { defineConfig } from 'vite'

export default defineConfig({
  css: {
    postcss: './postcss.config.js'
  }
})
```

### Next.js

```js
// postcss.config.js
module.exports = {
  plugins: {
    fuezcss: {},
    autoprefixer: {}
  }
}
```

### Vue / React / Svelte

FuezCSS works with any framework that supports a PostCSS pipeline. Add it to your `postcss.config.js` and import the generated CSS file in your entry point.

---

## 🧩 Extending the Theme

You can extend or override any default token in `fuez.config.js`:

```js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: '#6C47FF',
        'brand-light': '#A78BFA'
      },
      fontFamily: {
        display: ['Inter', 'sans-serif']
      }
    }
  }
}
```

---

## 📁 Project Structure

```
your-project/
├── src/
│   └── assets/
│       └── index.css       ← FuezCSS directives go here
├── fuez.config.js           ← Theme & plugin config
├── postcss.config.js        ← PostCSS pipeline
└── package.json
```

---

## 🤝 Contributing

Contributions are welcome! Please open an issue or submit a pull request.

1. Fork this repository
2. Create your feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m 'feat: add my feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a pull request

---

## 📄 License

MIT © [Azid Muhammad](https://github.com/AzidMuhammad)

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/AzidMuhammad">Azid Muhammad</a>
</p>
