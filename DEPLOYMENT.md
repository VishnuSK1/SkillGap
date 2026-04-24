# Deployment Guide

## Local production-style test

1. Copy `.env.example` to `.env`
2. Set `DATA_DIR=./data` in `.env`
3. Run:

```bash
npm install
npm start
```

The app will create `./data` on first boot and seed it from the repo JSON files if those runtime files do not exist yet.

Health check:

```bash
curl http://127.0.0.1:8080/api/health
```

## Railway

1. Push this project to GitHub.
2. Create a new Railway project from the repo.
3. Add a Volume and mount it at `/data`.
4. Set environment variables:

```env
DATA_DIR=/data
PORT=8080
DEMO_ADMIN_EMAIL=vkulathunkal@clarku.edu
DEMO_ADMIN_PASSWORD=12345678
DEMO_ADMIN_NAME=Vishnu Kulathunkal
GEMINI_API_KEY=your_key_here
ADZUNA_APP_ID=your_id_here
ADZUNA_APP_KEY=your_key_here
```

5. Start command:

```bash
npm start
```

6. Optional health check path:

```text
/api/health
```

## Render

1. Create a new Web Service from the repo.
2. Add a Persistent Disk and mount it at `/data`.
3. Set:

```env
DATA_DIR=/data
PORT=10000
```

4. Build command:

```bash
npm install
```

5. Start command:

```bash
npm start
```

6. Set the health check path to `/api/health`.

## Notes

- Static UI files are served by Express from the project root.
- Runtime data now lives in `DATA_DIR`.
- Auth users are stored in `DATA_DIR/users.json`.
- Seed data still ships with the repo, so first deploy starts with demo content.
- Sign-in and sign-up are now backed by the server, but session state is still a simple browser-stored login for demo use rather than production-grade authentication.
