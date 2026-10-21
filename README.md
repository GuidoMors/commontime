# Availability Planner Client

This folder contains the React, TypeScript, and Vite frontend. It requires the Express API in the sibling `availability-planner` repository; the client does not connect directly to SQLite.

## Run locally

1. Start the API from the backend repository using its README instructions. It listens on `http://localhost:4000`.
2. From this folder, install dependencies and start Vite:
   ```bash
   npm install
   npm run dev
   ```
3. Open the local URL printed by Vite (normally `http://localhost:5173`).

Leave `VITE_API_BASE_URL` unset for local development. Vite proxies `/api` requests to `http://localhost:4000`. The optional `.env.example` is a reference; you do not need to copy it to `.env` for local development.

## Deploy to Cloudflare Pages

Connect this folder to a Pages project. Configure:

- **Framework preset:** Vite
- **Build command:** `npm run build`
- **Build output directory:** `dist`
- **Root directory:** the repository root if this folder is its own repository; if the backend and client are in one monorepo, set this to `commontime`.
- **Environment variable:** `VITE_API_BASE_URL` = the public HTTPS origin of the deployed Express API, without a trailing slash or `/api` suffix (for example, `https://your-api.example.com`).

The API must be deployed separately on a Node.js host. Configure its `APP_URL` and `CORS_ORIGINS` to the exact Pages site origin. Credentialed cross-origin sessions require HTTPS and `SESSION_COOKIE_SAME_SITE=none` with `SESSION_COOKIE_SECURE=true`. A Pages site configured with `localhost` would make each visitor's browser look for an API on that visitor's own computer.

The backend uses a SQLite file, so its host must provide persistent storage for that file and run a single API instance. Deploying this frontend does not deploy or include the API or its database.

## Accounts

Signup requires only a username and password. Email is optional; accounts without an email address cannot use email-based password recovery.
