# Cinema POS

A cinema point-of-sale system built in Go — my first Go project, following [this YouTube tutorial](https://www.youtube.com/watch?v=CIIrR5daWL4).

The app lets users browse movies, hold seats, and confirm or release bookings. Seat holds are stored in Redis with an expiry, so they're automatically released if not confirmed in time.

## Stack

- **Go** — standard library `net/http` for routing, no framework
- **Redis** — stores bookings and seat hold sessions
- **Docker Compose** — runs Redis + Redis Commander locally

## Getting started

Start Redis:

```bash
docker compose up -d
```

Run the server:

```bash
go run ./cmd
```

The app is available at `http://localhost:8080`. Redis Commander (a web UI for inspecting Redis) runs at `http://localhost:8081`.

## API

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/movies` | List all movies |
| `GET` | `/movies/{movieID}/seats` | List seats for a movie |
| `POST` | `/movies/{movieID}/seats/{seatID}/hold` | Hold a seat |
| `PUT` | `/sessions/{sessionID}/confirm` | Confirm a booking |
| `DELETE` | `/sessions/{sessionID}` | Release a held seat |

## Project structure

```
cmd/        # Entry point
internal/
  booking/  # Domain, service, handler, Redis store
  adapters/ # Redis client wrapper
  utils/    # Shared utilities
static/     # Frontend (served as static files)
```
