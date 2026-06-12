# START_APP.md — how to run and probe this app

> **Build team:** fill in every `<...>` below once your app runs. Other teams use this file to
> start your app and probe it during Break. Keep it accurate — a break is filed against the app a
> breaker can actually start from these instructions.

## What this app is

- **App:** a notes / journal app with login (menu #2)
- **Stack:** Python + Flask (SQLite file storage)

## Start it

```bash
# 1. Install dependencies
python -m venv .venv && . .venv/bin/activate   # if you don't already have the venv
pip install -r requirements.txt

# 2. Run it
flask --app app run --port 8000
```

The database (`notes.db`) is created and seeded automatically on first run. To start from a
clean slate, delete `notes.db` and run again.

- **Base URL:** http://localhost:8000
- **Stop it:** Ctrl-C in the terminal running it.

## How to interact with it

- **Main endpoints / pages:**
  - `GET /` — your home page: lists your notes (when logged in) — `http://localhost:8000/`
  - `GET|POST /register` — create an account — form fields `username`, `password`
  - `GET|POST /login` — log in — form fields `username`, `password`
  - `GET /logout` — log out
  - `GET|POST /notes/new` — write a new note — form fields `title`, `body`
  - `GET /notes/<id>` — view a single note by numeric id — e.g. `http://localhost:8000/notes/2`
- **Accounts / credentials for legitimate use:** seeded demo account `demo` / `demo123`
  (there is also an `admin` / `admin123` account). You can also register your own.
- **A benign request that should succeed:**

  ```bash
  # log in as demo, then read demo's own note #2
  curl -s -c jar.txt -d "username=demo&password=demo123" http://localhost:8000/login
  curl -s -b jar.txt http://localhost:8000/notes/2
  ```

## For breakers

Attack this **running app over HTTP** — do **not** read this repo's source or `secret/` to find a
break. See [AGENTS_BREAK.md](AGENTS_BREAK.md) for the rules and your AI agent's instructions, and
[SPEC.md](SPEC.md) for the five properties (P1–P5) you are probing for.
