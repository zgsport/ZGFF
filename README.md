# ZG Sport Live — fresh three-site starter

This is a new project, separate from the old app. It contains three independent frontend apps and one shared API service:

- `ask/` — viewer question form
- `admin/` — private admin queue
- `overlay/` — transparent stream overlay
- `api/` — Express API and optional PostgreSQL persistence

## Important setup notes

This starter is not deployed yet. Before production use, set `API_URL` in each frontend's `config.js` to the real API service URL. Deploy each frontend as its own Render Static Site (publish directory `.` inside its folder) and deploy `api/` as a Render Web Service (`npm install`, `npm start`). Set `ADMIN_TOKEN` to a long random secret on the API service. Set `DATABASE_URL` to a Render PostgreSQL internal connection string for persistent storage. Without `DATABASE_URL`, the API uses in-memory storage, which resets when the service restarts.

Configure custom domains in Render:
- ask frontend: `ask.zgsport.live`
- admin frontend: `admin.zgsport.live`
- overlay frontend: `overlay.zgsport.live`

Add the DNS records Render provides at your domain registrar. Do not paste `ADMIN_TOKEN` into public frontend files. The admin token is entered into the admin login form and sent to API routes. For production, add rate limiting, stronger authentication/session handling, CSRF protections as appropriate, and restrict admin access. Use HTTPS.

## Current feature set

- Viewer submissions for start/sit and trade questions.
- Admin list with accept, decline, answer, and clear actions.
- Overlay polling, animated accepted/declined effects, and a small built-in set of ESPN NFL headshot IDs.
- A working `/health` API endpoint.

## Limitations to address before going live

- ESPN headshot IDs are only prefilled for a small sample of players; unknown names display without a photo. Verify all IDs before streaming.
- The database is shared by the API service. The three frontends are separate deployments, not three unrelated data stores.
- The API's simple token authentication is a starter, not a full production authentication system.
