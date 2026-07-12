# EV Stations Locator

A Django + Expo (React Native) application to find and browse electric vehicle (EV) charging stations. The backend provides a REST API (Django + DRF) and the frontend is a cross-platform mobile/web app built with Expo and TypeScript.

## Stack
- Languages: Python (backend), TypeScript (frontend), HTML/CSS for templates/assets
- Frameworks / runtimes:
  - Backend: Django (see backend/manage.py, backend/config/)
  - Frontend: Expo (React Native + TypeScript)
- Notable libraries: Django REST Framework (serializers.py present), Expo / React Native (package.json), TypeScript

## What’s in this repository
Top-level layout (important files and folders):

```
backend/             Django project and apps
  config/            Django project settings, ASGI/WSGI, top-level urls
  stations/          Station models, serializers, views, urls, tests
  users/             User models, serializers, auth/backends, urls
  charging_station/  (app folder - charging station related code)
  admin_panel/       (admin-related code)
  service_center/    (service center related code)
  showroom/          (showroom related code)
  templates/         Django HTML templates (if used)
  static/            static assets served by Django
  manage.py          Django management entrypoint

frontend/            Expo React Native app (TypeScript)
  app/                app source (screens, components)
  assets/             images & static assets used by the app
  context/            React context providers
  hooks/              custom React hooks
  services/           API clients and other services
  utils/               helper utilities
  package.json        frontend dependencies & scripts
  tsconfig.json       TypeScript config
  app.json / eas.json Expo configuration
README.md            (this file)
```

How it fits together:
- The Django backend exposes REST endpoints (see backend/config/urls.py and the per-app urls like backend/stations/urls.py). Data models and API serialization live in backend/stations/models.py and backend/stations/serializers.py.
- The frontend (Expo app) calls the backend API to list, search, and display charging stations. Frontend code lives under frontend/app and uses TypeScript.

## Quickstart — Backend (Django)
1. Create and activate a Python virtual environment:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate   # macOS / Linux
   .venv\Scripts\activate      # Windows (PowerShell)
   ```
2. Install dependencies (if there is a requirements file):
   ```bash
   pip install -r backend/requirements.txt
   ```
   If no requirements file is provided, install at least Django and DRF:
   ```bash
   pip install django djangorestframework
   ```
3. Apply migrations and create a superuser:
   ```bash
   python backend/manage.py migrate
   python backend/manage.py createsuperuser
   ```
4. Run the development server:
   ```bash
   python backend/manage.py runserver
   ```
5. Configuration:
   - Check `backend/config/settings.py` for database and environment variable configuration (e.g. SECRET_KEY, DEBUG, DATABASE settings). Adjust as needed for production.

## Quickstart — Frontend (Expo / React Native)
1. Install Node dependencies:
   ```bash
   cd frontend
   npm install
   # or
   yarn
   ```
2. Start the Expo dev server:
   ```bash
   npm run dev
   # or
   expo start
   ```
3. Run on a device / emulator:
   - Android: `expo run:android` or use the Expo Go app
   - iOS: `expo run:ios` or use the Expo Go app (macOS required for simulator)

Notes:
- See `frontend/package.json` for available scripts (build, lint, platform-specific commands).
- Check `app.json` / `eas.json` for Expo configuration and build settings.

## API & Code pointers
- API routing: `backend/config/urls.py` ties app routes together. Per-app routes are in each app's `urls.py` (for example `backend/stations/urls.py`).
- Business logic and endpoints:
  - Stations: models in `backend/stations/models.py`, API views in `backend/stations/views.py`, serialization in `backend/stations/serializers.py`.
  - Users: see `backend/users/` (models, serializers, auth/backends).
- Tests: Django tests can be run with:
  ```bash
  python backend/manage.py test
  ```

## Development tips
- Use environment variables for secrets and DB configuration. Inspect `backend/config/settings.py` to find which variables are consumed.
- The frontend is TypeScript; ensure your editor / CI runs `tsc` or the provided linter/typecheck scripts.
- If you plan to connect the Expo app to a local Django server, use an IP address reachable by your device/emulator (or use ngrok for tunneling).

## Contributing
- Open an issue for the feature/bug you intend to work on.
- Fork, create a feature branch, and submit a pull request with tests and a clear description.
- Follow existing code style (Django best practices for backend, idiomatic React/TypeScript for frontend).

## License
Include your preferred license (e.g., MIT). If you already have a LICENSE file in the repo, follow that.

## Questions you might want to answer next
- Which database is intended for production (check `backend/config/settings.py`) and are there migrations for it?
- How does the frontend authenticate with the backend (see `backend/users` and `frontend/services`)?
- Are there environment variable examples or a `.env.example` file to document required keys?
