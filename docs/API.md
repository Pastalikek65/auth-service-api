# API Reference

All error responses use the shape `{ "error": { "code": "string", "message": "string" } }`.

## Authentication

### POST /auth/register
Auth required: No. Registers a new user account.
```json
{ "id": "usr_123", "email": "user@example.com", "verified": false }
```
Error:
```json
{ "error": { "code": "conflict", "message": "Email already registered" } }
```

### POST /auth/login
Auth required: No. Authenticates a user and returns tokens.
```json
{ "accessToken": "eyJ...", "refreshToken": "eyJ...", "expiresIn": 900 }
```
Error:
```json
{ "error": { "code": "unauthorized", "message": "Invalid credentials" } }
```

### POST /auth/refresh
Auth required: No (refresh token). Issues a new access token.
```json
{ "accessToken": "eyJ...", "expiresIn": 900 }
```

### POST /auth/logout
Auth required: Yes. Revokes the current session.
```json
{ "success": true }
```

### POST /auth/forgot-password
Auth required: No. Sends a password reset email.
```json
{ "success": true }
```

### POST /auth/reset-password
Auth required: No. Resets a password using a reset token.
```json
{ "success": true }
```

### POST /auth/verify-email
Auth required: No. Verifies an email address using a token.
```json
{ "verified": true }
```

### POST /auth/resend-verification
Auth required: No. Resends the verification email.
```json
{ "success": true }
```

### POST /auth/change-password
Auth required: Yes. Changes the authenticated user password.
```json
{ "success": true }
```

## Two-Factor Auth

### POST /auth/2fa/enable
Auth required: Yes. Begins 2FA enrollment and returns a TOTP secret.
```json
{ "secret": "JBSWY3DPEHPK3PXP", "otpauthUrl": "otpauth://totp/..." }
```

### POST /auth/2fa/verify
Auth required: Yes. Verifies a TOTP code to activate 2FA.
```json
{ "enabled": true }
```

### POST /auth/2fa/disable
Auth required: Yes. Disables 2FA for the account.
```json
{ "enabled": false }
```

## Sessions

### GET /auth/sessions
Auth required: Yes. Lists active sessions.
```json
[ { "sessionId": "sess_1", "device": "Chrome", "createdAt": "2026-01-01T00:00:00Z" } ]
```

### DELETE /auth/sessions/:sessionId
Auth required: Yes. Revokes a specific session.
```json
{ "success": true }
```

## OAuth

### GET /auth/oauth/:provider
Auth required: No. Redirects to the OAuth provider.

### GET /auth/oauth/:provider/callback
Auth required: No. Handles the OAuth callback and returns tokens.
```json
{ "accessToken": "eyJ...", "refreshToken": "eyJ..." }
```

## User Management

### GET /users/me
Auth required: Yes. Returns the current user.
```json
{ "id": "usr_123", "email": "user@example.com", "role": "user" }
```

### PUT /users/me
Auth required: Yes. Updates the current user profile.
```json
{ "id": "usr_123", "name": "Jane Doe" }
```

### GET /users/:id
Auth required: Yes. Returns a user by id.
```json
{ "id": "usr_123", "email": "user@example.com" }
```

### POST /users
Auth required: Yes (admin). Creates a user.
```json
{ "id": "usr_456", "email": "new@example.com" }
```

### PUT /users/:id
Auth required: Yes (admin). Replaces a user record.
```json
{ "id": "usr_456", "email": "new@example.com" }
```

### PATCH /users/:id/role
Auth required: Yes (admin). Updates a user role.
```json
{ "id": "usr_456", "role": "admin" }
```

### GET /users
Auth required: Yes (admin). Lists users.
```json
[ { "id": "usr_123", "email": "user@example.com" } ]
```

### DELETE /users/:id
Auth required: Yes (admin). Deletes a user.
```json
{ "success": true }
```

## Roles & Permissions

### GET /roles
Auth required: Yes (admin). Lists roles.
```json
[ { "name": "admin", "permissions": ["users:read", "users:write"] } ]
```

### POST /roles
Auth required: Yes (admin). Creates a role.
```json
{ "name": "editor", "permissions": ["users:read"] }
```

## System

### GET /health
Auth required: No. Returns service health.
```json
{ "status": "ok", "uptime": 12345 }
```
