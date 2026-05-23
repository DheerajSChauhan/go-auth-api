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

## API Examples

Register a new user:

```bash
curl -X POST http://localhost:5000/register \
	-H "Content-Type: application/json" \
	-d '{"email":"test@example.com","password":"secret123"}'
```

Login and get a JWT:

```bash
curl -X POST http://localhost:5000/login \
	-H "Content-Type: application/json" \
	-d '{"email":"test@example.com","password":"secret123"}'
```

Use the returned token to call protected routes:

```bash
curl http://localhost:5000/api/files \
	-H "Authorization: Bearer YOUR_JWT_TOKEN"
```

Expected auth response shape:

```json
{
	"token": "eyJ...",
	"user": {
		"id": "66f...",
		"email": "test@example.com",
		"role": "user",
		"createdAt": "2026-05-23T12:00:00Z",
		"updatedAt": "2026-05-23T12:00:00Z"
	}
}
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
- Protected routes expect `Authorization: Bearer <token>`.
