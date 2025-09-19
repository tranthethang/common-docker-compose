# Development Tools Docker Compose

This Docker Compose setup provides a comprehensive development environment with multiple database systems, caching solutions, message queues, and development tools, all accessible through a Traefik reverse proxy.

## Services Included

### Databases
- **PostgreSQL 17 (pgvector)** - Primary relational database with vector search extension
- **MySQL 8.0** - Alternative relational database
- **MongoDB 8.0** - NoSQL document database

### Caching & Memory
- **Redis 7** - In-memory data structure store (alpine variant)
- **Memcached 1.6** - Distributed memory caching system (alpine variant)

### Message Queue
- **RabbitMQ 3.13** - Message broker with management interface (management-alpine)

### Development Tools
- **Traefik** - Reverse proxy and load balancer
- **Adminer 5** - Database management tool
- **Mailpit** - Modern email testing tool with advanced features
- **SonarQube LTS** - Code quality and security analysis
- **Portainer CE LTS** - Container management UI
- **MinIO** - S3 compatible object storage
- **Gitea** - Self-hosted Git service
- **Concourse** - CI/CD tool
- **Ollama** - Run large language models locally
- **AnythingLLM** - A private ChatGPT for your documents

## Quick Start

1. **Clone and navigate to the project directory**
   ```bash
   cd /path/to/your/project
   ```

2. **Copy the environment file**
   ```bash
   cp .env.example .env
   ```

3. **Configure your `/etc/hosts` file**
   Add the following lines to your `/etc/hosts` file to access the services via their hostnames:
   ```
   127.0.0.1 minio.localhost portainer.localhost adminer.localhost mailpit.localhost rabbitmq.localhost redisinsight.localhost anythingllm.localhost sonarqube.localhost gitea.localhost concourse.localhost
   ```

4. **Start all services**
   ```bash
   docker compose up -d
   ```

5. **Or start specific service groups using profiles**
   ```bash
   # Start only database services
   docker compose --profile database up -d
   
   # Start only cache services  
   docker compose --profile cache up -d
   
   # Start specific service
   docker compose --profile management up -d
   ```

6. **Check service status**
   ```bash
   docker compose ps
   ```

## Traefik Reverse Proxy

Traefik is used as a reverse proxy to manage access to the services. The Traefik dashboard is available at [http://localhost:8080](http://localhost:8080).

## Service Access

### Web Interfaces
- **Traefik Dashboard**: [http://localhost:8080](http://localhost:8080)
- **Adminer**: [http://adminer.localhost](http://adminer.localhost) - Database management
- **RabbitMQ Management**: [http://rabbitmq.localhost](http://rabbitmq.localhost) - Message queue management
- **Mailpit**: [http://mailpit.localhost](http://mailpit.localhost) - Email testing interface
- **MinIO Console**: [http://minio.localhost](http://minio.localhost) - Object storage UI
- **Portainer**: [http://portainer.localhost](http://portainer.localhost) - Container management UI
- **SonarQube**: [http://sonarqube.localhost](http://sonarqube.localhost) - Code quality analysis
  - Default credentials: `admin/admin`
  - ⚠️ **Important**: Change the default password after first login
- **RedisInsight**: [http://redisinsight.localhost](http://redisinsight.localhost) - Redis GUI
- **Gitea**: [http://gitea.localhost](http://gitea.localhost) - Git service
- **Concourse**: [http://concourse.localhost](http://concourse.localhost) - CI/CD
- **AnythingLLM**: [http://anythingllm.localhost](http://anythingllm.localhost) - Private ChatGPT

### SMTP Testing
- **Mailpit SMTP**: `localhost:1025`

## Configuration

### Environment Variables

Copy `.env.example` to `.env` and customize the following variables:

#### Generic
- `RESTART_POLICY` - Container restart policy (default: `always`)
- `TZ` - Timezone (default: `Asia/Ho_Chi_Minh`)

#### Traefik
- `MINIO_HOST`
- `PORTAINER_HOST`
- `ADMINER_HOST`
- `MAILPIT_HOST`
- `RABBITMQ_HOST`
- `REDISINSIGHT_HOST`
- `ANYTHINGLLM_HOST`
- `SONARQUBE_HOST`
- `GITEA_HOST`
- `CONCOURSE_HOST`

#### PostgreSQL
- `POSTGRES_USER`
- `POSTGRES_PASSWORD`
- `POSTGRES_DB`
- `POSTGRES_PORT`
- `POSTGRES_HOST`

#### MySQL
- `MYSQL_DATABASE`
- `MYSQL_USER`
- `MYSQL_PASSWORD`
- `MYSQL_ROOT_PASSWORD`
- `MYSQL_PORT`

#### MongoDB
- `MONGO_ROOT_USER`
- `MONGO_ROOT_PASSWORD`
- `MONGO_PORT`

#### Redis
- `REDIS_PASSWORD`
- `REDIS_PORT`

#### RabbitMQ
- `RABBITMQ_USER`
- `RABBITMQ_PASSWORD`
- `RABBITMQ_PORT`

#### Mailpit
- `MAILPIT_SMTP_PORT`

#### Memcached
- `MEMCACHED_PORT`

#### MinIO
- `MINIO_ROOT_USER`
- `MINIO_ROOT_PASSWORD`
- `MINIO_DEFAULT_BUCKETS`
- `MINIO_BROWSER`

#### Ollama
- `OLLAMA_PORT`
- `OLLAMA_MODEL`
- `OLLAMA_BASE_URL`

#### AnythingLLM
- `ANYTHINGLLM_STORAGE_DIR`
- `ANYTHINGLLM_DB_NAME`

#### Gitea
- `GITEA_DB_NAME`
- `GITEA_SSH_PORT`

#### Concourse
- `CONCOURSE_DB_NAME`
- `CONCOURSE_EXTERNAL_URL`
- `CONCOURSE_ADD_LOCAL_USER`
- `CONCOURSE_MAIN_TEAM_LOCAL_USER`
- `CONCOURSE_WORKER_GARDEN_NETWORK`

## Requirements

- Docker Engine 20.10+
- Docker Compose 2.0+
- At least 4GB RAM (recommended 8GB for SonarQube)
- Available ports: 80, 8080, 1025, 5432, 3306, 27017, 6379, 11211, 5672, 2222, 11434
