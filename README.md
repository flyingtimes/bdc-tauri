# BDC Tauri

A modern desktop application built with Tauri v2, Vue 3, and Tailwind CSS.

## Features

- 🚀 **Tauri v2**: Modern, secure desktop application framework
- ⚡ **Vue 3**: Progressive JavaScript framework with Composition API
- 🎨 **Tailwind CSS v4**: Utility-first CSS framework
- 🔧 **TypeScript**: Type-safe development
- 📱 **Multi-Platform**: Windows, Android, and macOS support

## Recommended IDE Setup

[VS Code](https://code.visualstudio.com/) + [Vue (Official)](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Recommended Browser Setup

- Chromium-based browsers (Chrome, Edge, Brave, etc.):
  - [Vue.js devtools](https://chromewebstore.google.com/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)
  - [Turn on Custom Object Formatter in Chrome DevTools](http://bit.ly/object-formatters)
- Firefox:
  - [Vue.js devtools](https://addons.mozilla.org/en-US/firefox/addon/vue-js-devtools/)
  - [Turn on Custom Object Formatter in Firefox DevTools](https://fxdx.dev/firefox-devtools-custom-object-formatters/)

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) to make the TypeScript language service aware of `.vue` types.

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Run Tauri Development Mode

```sh
npm run tauri:dev
```

### Build Tauri Application (Windows)

```sh
npm run tauri:build
```

## GitHub Actions CI/CD

This project includes automated GitHub Actions workflows for building across multiple platforms.

### Workflows

#### 1. **Build Workflow** (`.github/workflows/build.yml`)
Triggers on:
- Push to `main` or `release` branches
- Pull requests to `main`
- Manual workflow dispatch

Builds and uploads artifacts for:
- **Windows**: x86_64 (MSI installer + exe)
- **Android**: ARM64 APK
- **macOS Intel**: x86_64 (DMG + app bundle)
- **macOS Apple Silicon**: ARM64 (DMG + app bundle)

#### 2. **Release Workflow** (`.github/workflows/release.yml`)
Triggers on:
- Push version tags (e.g., `v1.0.0`)
- Manual workflow dispatch

Creates GitHub releases with:
- All platform builds uploaded to the release
- Automated version management
- Release notes generation

### Usage

#### Build All Platforms (CI)
Push to `main` branch to trigger automatic builds:
```bash
git add .
git commit -m "Trigger CI build"
git push origin main
```

Artifacts will be available in the Actions tab.

#### Create Release
To create a new release with all platform builds:

```bash
# Tag and push
git tag v1.0.0
git push origin v1.0.0
```

This will:
1. Build all platforms
2. Create/update GitHub release
3. Upload installers and bundles to the release

### Supported Platforms

| Platform | Architecture | Output Format |
|----------|-------------|---------------|
| Windows 10/11 | x86_64 | MSI installer, exe |
| Android | ARM64 | APK |
| macOS 11+ | Intel (x86_64), Apple Silicon (ARM64) | DMG, app bundle |

## Local Development

### Run Unit Tests with [Vitest](https://vitest.dev/)

```sh
npm run test:unit
```

### Run End-to-End Tests with [Cypress](https://www.cypress.io/)

```sh
npm run test:e2e:dev
```

This runs the end-to-end tests against the Vite development server.
It is much faster than the production build.

But it's still recommended to test the production build with `test:e2e` before deploying (e.g. in CI environments):

```sh
npm run build
npm run test:e2e
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

## Project Structure

```
bdc-tauri/
├── .github/
│   └── workflows/
│       ├── build.yml      # CI workflow for building all platforms
│       └── release.yml    # Release workflow for publishing
├── src/
│   ├── components/       # Vue components
│   ├── views/           # Vue views
│   └── assets/          # Static assets
├── src-tauri/
│   ├── gen/
│   │   └── android/       # Android project
│   ├── src/              # Rust source code
│   └── tauri.conf.json   # Tauri configuration
└── package.json
```

## License

[MIT](LICENSE)

## Acknowledgments

- [Tauri](https://tauri.app/)
- [Vue.js](https://vuejs.org/)
- [Tailwind CSS](https://tailwindcss.com/)
- [Vite](https://vitejs.dev/)
