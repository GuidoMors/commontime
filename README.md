# Availability Planner client

This repository contains the React, TypeScript, and Vite frontend. The API runs as a Cloudflare Worker and stores data in Cloudflare D1; the frontend does not connect directly to D1.

## Run locally

1. From the backend repository, follow its README to install dependencies, configure `server/.dev.vars`, and apply the local D1 migration.
2. Start the API from the backend repository:
   ```bash
   npm run dev
   ```
   Wrangler serves it at `http://localhost:8787`.
3. In this repository, install dependencies and start Vite:
   ```bash
   npm install
   npm run dev
   ```
4. Open `http://localhost:5173`.

Leave `VITE_API_BASE_URL` unset for local development. Vite proxies `/api` requests to the local Worker. For a deployed Pages site, set `VITE_API_BASE_URL` to the Worker HTTPS origin, with no trailing slash or `/api` suffix.

## Deploy to Cloudflare Pages

Connect this repository to Cloudflare Pages and configure:

- **Framework preset:** Vite
- **Build command:** `npm run build`
- **Build output directory:** `dist`
- **Root directory:** repository root
- **Environment variable:** `VITE_API_BASE_URL` = the deployed Worker URL, such as `https://availability-planner-api.<account>.workers.dev`

Set the Worker’s `CORS_ORIGINS` to the exact Pages origin. For `pages.dev` and `workers.dev` cross-origin requests, configure the Worker session cookie with `SameSite=None` and `Secure=true`. The browser API client sends credentials for cookie-based sessions.

Deploying this frontend does not deploy the Worker or migrate data; see the backend README for those steps.

## Accounts

Signup requires only a username and password. A one-time recovery key is displayed after signup; save it securely because it is needed to reset a forgotten password and cannot be retrieved later. Existing accounts need a recovery key supplied by the administrator; existing Argon2 accounts can also change to a Worker-compatible password from a preserved session.
