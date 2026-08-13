# Contributing

Thanks for your interest in improving the Auth Service API!

## Reporting Issues & Proposing Changes

Please open an issue to report bugs or propose changes before submitting large pull requests. Describe the problem, expected behavior, and steps to reproduce.

## Branch Naming

Use descriptive, prefixed branch names:

- `feature/*` for new functionality
- `fix/*` for bug fixes

## Commit Messages

This project follows [Conventional Commits](https://www.conventionalcommits.org/). Examples:

```
feat(auth): add refresh token rotation
fix(sessions): correct session expiry check
docs(api): document 2FA endpoints
```

## Running Postman Tests Locally

Install the Postman CLI:

```
curl -o- "https://dl-cli.pstmn.io/install/linux64.sh" | sh
```

Then run the collection:

```
postman collection run "postman/auth-service-api.postman_collection.json" -e "postman/auth-service-local.postman_environment.json"
```

## Code of Conduct

Be respectful and constructive. Harassment or abusive behavior of any kind will not be tolerated.
