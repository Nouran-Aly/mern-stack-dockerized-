# mern-docker

A fully dockerized MERN stack application (MongoDB, Express, React, Node.js) built from scratch for learning purposes.

## Stack

- **Frontend** — React + Vite, served on port 5173
- **Backend** — Node.js + Express API, running on port 5050
- **Database** — MongoDB, data persisted via Docker named volume

## Prerequisites

- Docker
- Docker Compose

## Getting started

Clone the repo and bring the stack up with a single command:

```bash
git clone https://github.com/Nouran-Aly/mern-stack-dockerized-.git
cd mern-docker
docker compose up --build
```

| Service | URL |
|---|---|
| Frontend | http://localhost:5173 |
| Backend API | http://localhost:5050 |
| MongoDB | mongodb://localhost:27017 |

To stop everything:

```bash
docker compose down
```

To stop and wipe the database:

```bash
docker compose down -v
```

## Project structure

```
mern-docker/
├── frontend/
│   ├── Dockerfile
│   └── ...
├── backend/
│   ├── Dockerfile
│   └── ...
└── docker-compose.yml
```

## Architecture

```
browser
  │
  ├── :5173 → frontend container (React)
  │
  └── :5050 → backend container (Express)
                    │
                    └── mongo:27017 → mongodb container (internal network only)
```

All three services run on a dedicated Docker bridge network called `mern`. The frontend and backend are accessible from the host. MongoDB is only reachable internally by the backend — it is not exposed to the internet in production.

MongoDB data is stored in a named Docker volume (`mongo-data`) so it survives container restarts and `docker compose down`.

## Docker concepts covered

- Multi-container orchestration with Docker Compose
- Custom bridge networking with service name DNS resolution
- Named volumes for database persistence
- Bind mounts for live code sync in development
- Environment variables for service configuration
- `depends_on` for startup ordering


## Notes

This project was rebuilt from scratch based on an existing GitHub project, with the goal of understanding every line rather than copying. All Docker configuration was written and debugged manually.