# Omshree Medicals – Node.js + Express server

## Setup
1. Install Node 20+ and PostgreSQL.
2. `cd server && npm install`
3. Copy `.env.example` to `.env` and fill in values.
4. `npm run db:init` (creates tables)
5. `npm run dev` -> API at http://localhost:4000

All endpoints from the build guide are under `/api`. Every route except
`/api/auth/signup` and `/api/auth/login` needs `Authorization: Bearer <token>`.
Bill numbers (sequential, YYYYMMDD-001, IND-YYYY-0001, INV-YYYY-0001) are generated
server-side in a transaction with a per-user lock.

AI bill reading: `AI_PROVIDER=ollama` (run `ollama pull llama3.2-vision`) or `openai` with `OPENAI_API_KEY`.
Offline sync: `POST /api/sync` with `{changes:[{client_id,op,entity:"bills",payload}]}`;
creates are idempotent when the client sends the bill `id` (uuid).
Deploy: Render/Railway (Node service + Postgres).
