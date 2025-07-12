# Bitnami Docker Compose Stack

This repository contains Docker Compose configurations for running popular databases and message brokers using Bitnami and official images. Each service is isolated in its own directory with a dedicated `docker-compose` YAML file for easy management and deployment.

## Directory Structure

- `mongodb/` — MongoDB and Redis (as secondary service)
- `mysql/` — MySQL
- `postgresql/` — PostgreSQL
- `rabbitmq/` — RabbitMQ
- `redis/` — Standalone Redis

## Services Overview

### MongoDB & Redis
- **MongoDB**: Runs the latest MongoDB image with authentication enabled. Data is persisted to `./docker/mongodb_data`. Initialization script support via `init-mongo.js`.
- **Redis**: Runs the latest Redis image, persists data to `./docker/redis_data`.
- **Network**: Both run on a custom Docker bridge network.

### MySQL
- **Image**: Bitnami MySQL 9.3
- **Ports**: 3306
- **Volumes**: Data persisted to `./mysql_data`
- **Environment**: Configurable root/user credentials and database name via environment variables.

### PostgreSQL
- **Image**: Bitnami PostgreSQL (latest)
- **Ports**: 5432
- **Volumes**: Data persisted to `./pg_docker/postgresql_data`
- **Environment**: Configurable root/user credentials and database name via environment variables.

### RabbitMQ
- **Image**: Bitnami RabbitMQ 4.1
- **Ports**: 15672 (management UI)
- **Volumes**: Data persisted to `./rabbitmq_data`
- **Environment**: Configurable username, password, and Erlang cookie via environment variables.

### Redis (Standalone)
- **Image**: Bitnami Redis (latest)
- **Ports**: 6379
- **Environment**: Password protected, disables dangerous commands (`FLUSHDB`, `FLUSHALL`).

## Usage

1. **Configure Environment Variables:**
   - Copy the sample `.env` files (if provided) or create your own in each directory with the required variables (see each compose file for details).

2. **Start Services:**
   ```sh
   docker-compose -f <service-directory>/<compose-file> up -d
   ```
   Example for MySQL:
   ```sh
   docker-compose -f mysql/docker.myql.compose.yml up -d
   ```

3. **Stop Services:**
   ```sh
   docker-compose -f <service-directory>/<compose-file> down
   ```

4. **Data Persistence:**
   - Data for each service is stored in local directories mapped as volumes. These persist even after containers are stopped or removed.

## Notes
- All images are sourced from Bitnami or official Docker repositories.
- Adjust environment variables as needed for your development or production needs.
- For advanced configuration, refer to the official Bitnami documentation for each service.

## License
This repository is provided under the [APACHE-2.0](https://www.apache.org/licenses/LICENSE-2.0) license.
