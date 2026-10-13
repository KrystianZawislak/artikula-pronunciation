# ARTIKULA — Speech Therapy Studio

Landing page and booking system for a fictional speech therapy studio in Kraków. A single-page frontend with a scroll-driven canvas animation talks to a Laravel REST API secured with Sanctum. The site content is in Polish.

Built as a learning project for Laravel, REST APIs and the OWASP Top 10.

## Stack

- **Backend:** PHP 8.3+, Laravel 13, Sanctum (SPA cookie auth), Eloquent
- **Database:** SQLite (default) or MySQL
- **Frontend:** HTML, CSS, jQuery, with no build step
- **Tests:** PHPUnit feature tests

## Getting started

```bash
cd app
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate --seed
php artisan serve
```

Open http://localhost:8000.

To test on a phone over Wi-Fi, run `php artisan serve --host=0.0.0.0` and add your machine's IP to `SANCTUM_STATEFUL_DOMAINS` in `.env`.

## API

| Method | Endpoint | Auth |
|---|---|---|
| `POST` | `/api/register`, `/api/login` | rate-limited (6/min) |
| `GET` | `/api/services` | public |
| `POST` | `/api/logout` | ✓ |
| `GET` | `/api/user` | ✓ |
| `GET` `POST` | `/api/appointments` | ✓ |
| `PUT` `DELETE` | `/api/appointments/{id}` | ✓ owner only |

## Security highlights

- Cookie-based Sanctum auth with CSRF protection, so no tokens are stored in `localStorage`
- Ownership enforced via `AppointmentPolicy`
- Rate limiting on login and registration
- Slot-conflict validation and a limit of 3 appointments per user
- Eloquent only, with no raw SQL

## Tests

```bash
cd app && php artisan test
```

The tests cover registration, login, appointment CRUD, validation, ownership checks and the appointment limit.

## Docs

More detailed guides live in [`docs/`](docs/): setup, project structure, database commands and an explanation of the tests.
