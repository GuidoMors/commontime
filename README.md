# Availability Planner Client

Standalone React + TypeScript client. Deploy this folder as a Cloudflare Pages project:

- Framework preset: Vite
- Build command: `npm run build`
- Build output directory: `dist`
- Build environment variable: `VITE_API_BASE_URL`, set to the API origin (for example `https://localhost:4443` when testing the deployed site against an HTTPS reverse proxy on the same computer)

For local development, leave `VITE_API_BASE_URL` unset and run `npm run dev`. Vite proxies `/api` requests to `http://localhost:4000`.

The browser makes API requests directly. A deployed Pages site using `localhost` reaches the backend on the visitor's computer. It does not make the backend public or let other visitors access the developer's computer. The backend must allow the Pages origin in `CORS_ORIGINS`; credentialed cross-origin sessions require HTTPS and `SameSite=None` cookies. See the server repository's README for the corresponding API configuration.
