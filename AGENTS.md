# AGENTS.md — Todo App

## Project Overview

A cloud-synced Todo List app built with **React 18** + **Material UI (MUI) v5** + **Firebase Realtime Database**. Single-file architecture, no build tools required.

## Tech Stack

- **Frontend:** React 18 (UMD), Material UI v5, Babel standalone (in-browser JSX transform)
- **Backend:** Firebase Realtime Database (asia-southeast1)
- **Hosting:** GitHub Pages (chengyukpong.github.io/todo-app)
- **Styling:** MUI dark theme, CSS gradient background, Inter font

## Architecture

```
todo-app/
├── index.html          # Entire app (HTML + CSS + React + Firebase) — single file
├── firebase-rules.json # Firebase security rules (reference copy)
├── AGENTS.md           # This file
└── README.md           # (optional) GitHub description
```

**Key constraint:** This is a single `index.html` file. All code (React components, Firebase config, styles) lives inline. No bundler, no `package.json`, no `node_modules`.

## Firebase Setup

- **Project ID:** `todo-app-5dad1`
- **Database URL:** `https://todo-app-5dad1-default-rtdb.asia-southeast1.firebasedatabase.app`
- **Region:** asia-southeast1
- **Data path:** `/todos/{todoId}`

### Data Schema

```json
{
  "todos": {
    "<auto-id>": {
      "text": "Buy groceries",
      "done": false,
      "createdAt": "2026-04-23T08:43:06.887Z"
    }
  }
}
```

### Security Rules

See `firebase-rules.json`. Current rules:
- Read/write allowed on `/todos` only
- Each todo must have `text` (string, 1-500 chars), `done` (boolean), `createdAt` (string)
- No extra fields allowed
- All other paths denied

## How to Develop

1. Edit `index.html` directly
2. Test locally: `python3 -m http.server 8080` in this directory
3. Deploy: push to `main` branch → GitHub Pages auto-deploys

### CDN Dependencies (loaded in HTML)

```
react@18, react-dom@18       — UI framework
@babel/standalone             — JSX → JS transform
@mui/material@5               — component library
firebase@10.12.0 (app+db)    — realtime database
```

## Common Tasks

### Add a new feature
- Edit the `<script type="text/babel">` block in `index.html`
- Components are plain React functions using MUI components

### Update Firebase rules
- Edit `firebase-rules.json` locally (reference)
- Update in Firebase Console → Realtime Database → Rules → Publish

### Change theme/colors
- Modify the `createTheme()` call in the React code
- Gradient background is in the `<style>` block

### Add Firebase Auth
- Add `firebase-auth-compat.js` CDN script
- Update rules to require `auth != null`
- Add login UI (Google sign-in recommended)

## Gotchas

- Firebase API key is client-side by design — security comes from **database rules**, not hiding the key
- Babel standalone is ~1.8MB — fine for a single-page app but not for larger projects
- GitHub Pages caches aggressively — may need hard refresh after deploy
- No TypeScript, no linting — keep it simple
