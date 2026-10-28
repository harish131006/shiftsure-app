# ShiftSure — Gamified Attendance & Fair Work Tracker

ShiftSure is a local, demo-ready attendance prototype for small businesses. It includes employee and manager roles, SQLite persistence, real clock-in/clock-out workflows, correction approvals, CSV exports, and simple gamification badges.

> This is a **working prototype**, not a production-ready system. Run it only with the supplied sample data and change all credentials/secrets before any real deployment.

## Tech stack

- **Frontend:** React 18 + Vite, React Router, plain CSS
- **Backend:** Node.js + Express
- **Database:** SQLite via `better-sqlite3`
- **Auth:** JWT access tokens and bcrypt password hashing
- **Validation:** Zod
- **Tests:** Vitest and Supertest

## Demo credentials

| Role | Email | Password |
|---|---|---|
| Manager | manager@shiftsure.demo | Manager@123 |
| Employee | arjun@shiftsure.demo | Employee@123 |
| Employee | priya@shiftsure.demo | Employee@123 |
| Employee | kavin@shiftsure.demo | Employee@123 |

## Windows setup — beginner friendly

1. Install **Node.js 20 LTS or newer** from https://nodejs.org/.
2. Extract this ZIP.
3. Open **Command Prompt** in the extracted folder.
4. Install and prepare the backend:

```bat
cd server
npm install
copy .env.example .env
npm run db:init
npm run db:seed
```

5. Start the backend:

```bat
npm run dev
```

Leave this window open. The API runs at `http://localhost:4000`.

6. Open a **second Command Prompt** in the extracted folder and start the frontend:

```bat
cd client
npm install
npm run dev
```

7. Open the URL shown by Vite, normally `http://localhost:5173`.

## Useful commands

```bat
cd server
npm test
```

```bat
cd client
npm test
```

The database file is created at `server/data/shiftsure.db`. Delete it and rerun the initialization and seed commands to reset the demo.

## Demonstration checklist

1. Log in as `manager@shiftsure.demo` / `Manager@123`.
2. Review Today’s attendance, late arrivals, missing punches, statistics, employee records, correction requests, and settings.
3. Use search, date and status filters, then download the CSV timesheet.
4. Log out and log in as `arjun@shiftsure.demo` / `Employee@123`.
5. Clock in, refresh, confirm duplicate clock-in is blocked, then clock out.
6. Check live status, worked hours, attendance history, punctuality streak, and badges.
7. Submit an attendance-correction request.
8. Return to the manager account, approve or reject it, and verify the audit trail and updated attendance record.

## Architecture

See `docs/ARCHITECTURE.md` and `docs/API.md`.

## Security notes

- Passwords are hashed with bcrypt.
- Routes require a JWT; manager-only routes check the user role.
- Inputs are validated with Zod.
- The frontend stores the JWT in `localStorage`, which is acceptable for a local prototype but not ideal for production.
- For production, add HTTPS, rate limiting, refresh-token rotation, CSRF protection where applicable, structured logging, backups, and a security review.
