# go-auth-api

Go-based authentication API built with Gin, MongoDB, and JWT.

## Requirements

- Go 1.26.2 or newer
- MongoDB instance
- A JWT secret value

## Setup

Create a `.env` file in the project root with the following values:

```env
MONGO_URI=mongodb://localhost:27017
MONGO_DB_NAME=go_auth
JWT_SECRET=change-me
```

## Run

Start the API:

```bash
go run ./cmd/api
```

The server listens on `:5000`.

Optional live reload with Air:

```bash
air
```

## Available Routes

- `GET /health` - health check
- `POST /register` - create a user
- `POST /login` - sign in and receive a JWT
- `GET /api/files` - protected route that returns the current user id
- `GET /api/products` - protected route
- `GET /api/admin/resctricted` - admin-only route

## Notes

- Environment variables are loaded automatically from `.env`.
- The protected routes require a valid JWT in the request context.
