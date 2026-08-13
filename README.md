# Auth Service API

![License: MIT](https://img.shields.io/badge/license-MIT-green) ![Built with Postman](https://img.shields.io/badge/built%20with-Postman-orange)

A production-style JWT authentication and user management API, fully designed, mocked, and tested in Postman. It provides secure sign-up and sign-in flows, token lifecycle management, two-factor authentication, session control, social login, and role-based administration.

## Features

- JWT access and refresh tokens
- Email verification
- Password reset and password change
- Two-factor authentication (TOTP / 2FA)
- Session management
- OAuth social login
- Role-based access control (RBAC)
- Admin user CRUD
- Health check endpoint

## Tooling

The API contract was designed, mocked, and tested entirely in Postman. A Postman mock server backs the contract during development, and an hourly Postman monitor continuously exercises the collection to catch regressions.

## Getting Started

1. Import the collection from the `postman/` directory.
2. Select the appropriate environment.
3. Run the **Login** request to obtain access and refresh tokens, which are automatically saved to environment variables by the request test scripts.

## API Overview

### Authentication
- `POST /auth/register`
- `POST /auth/login`
- `POST /auth/refresh`
- `POST /auth/logout`
- `POST /auth/forgot-password`
- `POST /auth/reset-password`
- `POST /auth/verify-email`
- `POST /auth/resend-verification`
- `POST /auth/change-password`

### Two-Factor Auth
- `POST /auth/2fa/enable`
- `POST /auth/2fa/verify`
- `POST /auth/2fa/disable`

### Sessions
- `GET /auth/sessions`
- `DELETE /auth/sessions/:sessionId`

### OAuth
- `GET /auth/oauth/:provider`
- `GET /auth/oauth/:provider/callback`

### User Management
- `GET /users/me`
- `PUT /users/me`
- `GET /users/:id`
- `POST /users`
- `PUT /users/:id`
- `PATCH /users/:id/role`
- `GET /users`
- `DELETE /users/:id`

### Roles & Permissions
- `GET /roles`
- `POST /roles`

### System
- `GET /health`

## Error Handling

All errors return a consistent shape:

```json
{ "error": { "code": "string", "message": "string" } }
```

| Status | Meaning |
| ------ | ------- |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 429 | Too Many Requests |
| 500 | Internal Server Error |

## Testing

Every request ships with automated tests. Run them via the Postman Collection Runner, the scheduled monitor, or in CI using the Postman CLI.

## Project Structure

```
.
 README.md
 LICENSE
 .gitignore
 CONTRIBUTING.md
 docs/
    API.md
 .github/
     workflows/
         postman-api-tests.yml
```

## License

MIT License. Copyright (c) 2026 Aydin.
