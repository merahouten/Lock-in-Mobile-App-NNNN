# Lock-in-Mobile-App

Monorepo scaffold for LOCKIN MVP.

Structure:

- /mobile — Expo React Native minimal app
- /server — Node.js (Express) backend stub

Next steps:
1. Add OpenAPI spec for core endpoints (auth, onboarding, tasks, ai)
2. Add DB (Postgres) + ORM (Prisma) and migrations
3. Implement auth (OTP) + onboarding analysis job
4. Wire Execution AI (nightly job) and Notification scheduler
5. Add CI and basic tests

Continuous Integration

- A GitHub Actions workflow is included at `.github/workflows/ci.yml` which runs on push and pull requests to `main`.
  - **Server**: installs dependencies, runs `npx prisma generate` and `npx prisma db push` against `DATABASE_URL=file:./dev.db`, builds TypeScript, and runs `npm test`.
  - **Mobile**: installs dependencies and runs `npm run lint`.

Environment notes:
- For local dev, use Postgres via `docker compose up -d` and set `DATABASE_URL` in `server/.env`.
- To enable real SMS sending set `TWILIO_ACCOUNT_SID`, `TWILIO_AUTH_TOKEN`, `TWILIO_FROM` in `server/.env`.
- To enable real email sending set `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASS` in `server/.env`.

Quick commands

- Install deps for both packages: `npm run install:all`
- Start server + mobile concurrently (uses Expo tunnel): `npm run start:dev`

Notes:
- `npm run start:dev` uses `concurrently` to start `server` (`npm run dev`) and `mobile` (`npm run start:dev`) at the same time. It uses `npx` so it works without prior global installation of `concurrently`.

