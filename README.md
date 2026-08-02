# SchemaForge Desktop

A native desktop wrapper around SchemaForge, built with [Electron](https://www.electronjs.org/).

## What's in here

- `main.js` — the Electron main process (creates the app window, loads `src/index.html`)
- `src/index.html` — your SchemaForge app, unmodified
- `package.json` — has the `electron-builder` config for Windows (`.exe` installer), macOS (`.dmg`), and Linux (`.AppImage`)
- `.github/workflows/build.yml` — a GitHub Actions workflow that builds all three platforms automatically

## Run it locally (no packaging, just to try it)

```bash
npm install
npm start
```

## Build an installer

You can only reliably build for the OS you're building the DMG/EXE for macOS/Windows-specific
signing tools without extra setup, so the easiest path is:

### Option A — GitHub Actions (recommended, builds all 3 platforms for you)

1. Push this folder to a new GitHub repo.
2. Push a tag: `git tag v1.0.0 && git push --tags` (or just run the workflow manually from the
   Actions tab — it's set to `workflow_dispatch` too).
3. GitHub Actions will build on real Windows, macOS, and Linux runners and upload the installers
   as workflow artifacts — download them from the Actions run page.

### Option B — Build locally on each OS

On a Windows machine:
```bash
npm install
npm run dist:win      # → release/SchemaForge Setup 1.0.0.exe
```

On a Mac:
```bash
npm install
npm run dist:mac       # → release/SchemaForge-1.0.0.dmg
```

On Linux:
```bash
npm install
npm run dist:linux     # → release/SchemaForge-1.0.0.AppImage
```

## Already-built Linux version

`release/SchemaForge-1.0.0.AppImage` in this package was already built and verified to launch
correctly. Just:

```bash
chmod +x SchemaForge-1.0.0.AppImage
./SchemaForge-1.0.0.AppImage
```

(Needs FUSE installed on the host — most desktop Linux distros have this already. If not:
`sudo apt install libfuse2` on Debian/Ubuntu.)

## Adding a real icon

Right now the app uses Electron's default icon. To brand it:
1. Make a 512×512 PNG logo.
2. Convert it to `.ico` (Windows) and `.icns` (macOS) — e.g. with https://cloudconvert.com or the
   `electron-icon-builder` npm package.
3. Put them at `build/icon.ico`, `build/icon.icns`, `build/icon.png` and uncomment the `icon` lines
   in `package.json`'s `build` section and in `main.js`.
