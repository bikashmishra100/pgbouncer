# PgBouncer Docker image (Debian 12)

This image **builds PgBouncer from the source code** in this repository instead of using a prebuilt tarball.

## Building

Build from the **repository root** so the builder can access the full source tree:

```bash
# From the pgbouncer repo root
docker build -f debian-12/Dockerfile -t pgbouncer:local .
```

Or with Docker Compose (also from repo root):

```bash
docker-compose -f debian-12/docker-compose.yml build
```

## Running

See the main Bitnami PgBouncer image documentation for environment variables and usage. The image layout and entrypoint are unchanged; only the PgBouncer binary is built from source.

### Using a local PostgreSQL

To run PgBouncer against a PostgreSQL instance on the host with two database entries (`postgres1` and `postgres2`) pointing at the same backend:

1. Ensure local Postgres is running (e.g. db=`postgres`, user=`default`, password=`strongpassword`).
2. From the repo root:

   ```bash
   docker compose -f debian-12/docker-compose.local.yml up --build
   ```

3. Connect via PgBouncer on port 6432:

   ```bash
   psql -h localhost -p 6432 -U default -d postgres1   # or -d postgres2
   ```

Edit `debian-12/docker-compose.local.yml` to change host, user, password, or database names.
