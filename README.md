# Local PostgreSQL with Docker

A minimal PostgreSQL development environment powered by Docker Compose.

The goal is to keep the host OS clean: no native PostgreSQL installation, no background database service, and no need for a heavy GUI client. Run PostgreSQL in a container and connect to it from a lightweight VS Code extension or any PostgreSQL client.

> Intended for local development, not production deployment.

## Why Docker?

- Keeps PostgreSQL isolated from the host system.
- Makes the database version and setup reproducible.
- Avoids conflicts between projects that need different versions.
- Keeps database data persistent in a Docker volume.
- Makes the environment easy to start, stop, and remove.

## Requirements

- Docker
- Docker Compose
- Optional: a PostgreSQL-compatible VS Code extension

## Quick Start

```bash
git clone https://github.com/MostafaNasrollahpour/local-postgres-docker.git
cd local-postgres-docker
cp .env.example .env
docker compose up -d
```

Default connection values:

| Setting | Value |
| --- | --- |
| Host | `localhost` |
| Port | `5432` |
| Database | `devdb` |
| Username | `devuser` |
| Password | `devpassword` |

Change these values in `.env` when needed. The real `.env` file is ignored by Git.

## Common Commands

```bash
# Start
docker compose up -d

# Check status
docker compose ps

# View logs
docker compose logs -f postgres

# Stop (data is preserved)
docker compose down

# Reset everything, including database data
docker compose down -v
```

Be careful with `docker compose down -v`: it deletes the PostgreSQL volume and its data.

## Development with Containers

This workflow is not limited to databases. The same idea can keep other development dependencies and runtime versions off the host OS.

Examples:

```bash
# Redis
docker run --rm -p 6379:6379 redis:7-alpine

# Node.js 20
docker run --rm node:20 node --version

# Python 3.12
docker run --rm python:3.12 python --version

# .NET 8 SDK
docker run --rm mcr.microsoft.com/dotnet/sdk:8.0 dotnet --info
```

For larger projects, these services can be added to the same Compose setup so the whole development environment can be reproduced with minimal host configuration.

## License

This project is licensed under the [MIT License](LICENSE).
