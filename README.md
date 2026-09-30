# RustFS

> [!WARNING]
> This repository is work in progress, its content could change at any time.

[RustFS](https://rustfs.com) S3-compatible object store based on docker compose for experimenting and short workshops.

- S3 API: container port `9000`
- Web console: container port `9001`, path `/rustfs/console/`
- Data and logs: bind-mounted from the host (by default under `/data/storage/rustfs/`)

## Setup

1. Create the local configuration and set the credentials:

   ```bash
   cp .env.example .env
   openssl rand -hex 12      # -> RUSTFS_ACCESS_KEY
   openssl rand -base64 30   # -> RUSTFS_SECRET_KEY
   ```

   Edit `.env` and paste in the generated values. `.env` is git-ignored: never commit it.

2. Create the host directories. The container runs as uid/gid `10001`:

   ```bash
   sudo mkdir -p /data/storage/rustfs/data /data/storage/rustfs/logs
   sudo chown -R 10001:10001 /data/storage/rustfs
   ```

3. Start the service:

   ```bash
   docker compose up -d
   ```
