# Docker Cheatsheet

## Table of Contents

- [Docker Basics](#docker-basics)
- [Docker Images](#docker-images)
- [Docker Containers](#docker-containers)
- [Docker Compose](#docker-compose)
- [Docker Buildx](#docker-buildx)
- [Docker Init](#docker-init)
- [Docker Scout](#docker-scout)
- [Docker Networking](#docker-networking)
- [Docker Volumes](#docker-volumes)
- [Logging & Monitoring](#logging--monitoring)
- [Cleanup & Maintenance](#cleanup--maintenance)
- [Production Best Practices](#production-best-practices)
- [Advanced Commands](#advanced-commands)

## Docker Basics

| Command | Description |
|---------|-------------|
| `docker --version` | Show Docker version |
| `docker version` | Show detailed version info |
| `docker info` | Display system-wide information |
| `docker help` | List available commands |
| `docker COMMAND --help` | Get help for specific command |
| `docker debug` | Debug containers and images |

## Docker Images

### Building & Managing Images

| Command | Description |
|---------|-------------|
| `docker build -t name:tag .` | Build image from Dockerfile |
| `docker build --no-cache -t name:tag .` | Build without using cache |
| `docker build --platform=linux/amd64 -t name:tag .` | Build for specific platform |
| `docker build --secret id=key,src=./secret.txt .` | Build with secrets |
| `docker build --ssh default .` | Build with SSH agent forwarding |
| `docker build --progress=plain -t name:tag .` | Show plain build progress |
| `docker buildx build --load -t name:tag .` | Build with Buildx and load locally |
| `docker images` | List all images |
| `docker images -q` | List image IDs only |
| `docker images --format "table {{.Repository}}\t{{.Tag}}\t{{.Size}}"` | Format output |
| `docker image ls --filter="dangling=true"` | List dangling images |
| `docker rmi image_id` | Remove image |
| `docker image rm $(docker images -q)` | Remove all images |
| `docker image prune` | Remove unused images |
| `docker image prune -a --filter="until=24h"` | Remove images older than 24h |

### Registry Operations

| Command | Description |
|---------|-------------|
| `docker pull image:tag` | Pull image from registry |
| `docker pull --platform=linux/arm64 image:tag` | Pull for specific platform |
| `docker push image:tag` | Push image to registry |
| `docker login` | Login to Docker Hub |
| `docker login registry.example.com` | Login to private registry |
| `docker logout` | Logout from Docker Hub |
| `docker tag source:tag target:tag` | Tag an image |
| `docker search term` | Search Docker Hub |
| `docker manifest inspect image:tag` | Inspect image manifest |

## Docker Containers

### Running Containers

| Command | Description |
|---------|-------------|
| `docker run image` | Run container from image |
| `docker run -d image` | Run in detached mode |
| `docker run -it image` | Run with interactive terminal |
| `docker run --rm image` | Auto-remove after exit |
| `docker run --init image` | Use init process |
| `docker run --platform=linux/amd64 image` | Run on specific platform |
| `docker run -p host:container image` | Map ports |
| `docker run -P image` | Map all exposed ports |
| `docker run --expose=8080 image` | Expose additional port |
| `docker run -v host:container image` | Mount bind volume |
| `docker run --mount type=bind,src=/host,dst=/container image` | Mount using --mount |
| `docker run -e VAR=value image` | Set environment variable |
| `docker run --env-file .env image` | Load env from file |
| `docker run --name container_name image` | Set container name |
| `docker run --hostname=custom image` | Set container hostname |
| `docker run --restart=unless-stopped image` | Auto-restart policy |
| `docker run --memory=1g --cpus=0.5 image` | Set resource limits |
| `docker run --oom-kill-disable image` | Disable OOM killer |
| `docker run --ulimit nofile=65535:65535 image` | Set ulimits |

### Container Management

| Command | Description |
|---------|-------------|
| `docker ps` | List running containers |
| `docker ps -a` | List all containers |
| `docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Status}}"` | Format output |
| `docker ps --filter="status=running"` | Filter by status |
| `docker ps --filter="ancestor=image"` | Filter by image |
| `docker start container_id` | Start stopped container |
| `docker start -a container_id` | Start and attach |
| `docker stop container_id` | Stop running container |
| `docker stop -t 30 container_id` | Stop with custom timeout |
| `docker restart container_id` | Restart container |
| `docker pause container_id` | Pause container |
| `docker unpause container_id` | Unpause container |
| `docker kill container_id` | Force kill container |
| `docker kill -s SIGTERM container_id` | Kill with specific signal |
| `docker wait container_id` | Wait for container to stop |
| `docker rm container_id` | Remove container |
| `docker rm -f container_id` | Force remove running container |
| `docker container prune` | Remove stopped containers |

### Container Interaction

| Command | Description |
|---------|-------------|
| `docker exec -it container_id /bin/bash` | Enter container shell |
| `docker exec -it container_id sh` | Enter with sh (Alpine) |
| `docker exec -u root -it container_id bash` | Enter as root |
| `docker exec -w /app -it container_id bash` | Enter with working directory |
| `docker exec -it container_id command` | Execute command in container |
| `docker cp file container_id:/path` | Copy file to container |
| `docker cp container_id:/path file` | Copy file from container |
| `docker cp -a container_id:/path .` | Copy preserving attributes |
| `docker attach container_id` | Attach to running container |
| `docker attach --no-stdin container_id` | Attach without stdin |

### Container Inspection

| Command | Description |
|---------|-------------|
| `docker inspect container_id` | Inspect container details |
| `docker inspect --format='{{.State.Status}}' container_id` | Get specific field |
| `docker stats` | Show resource usage stats |
| `docker stats --no-stream` | Get stats snapshot |
| `docker stats container_id` | Show stats for specific container |
| `docker top container_id` | Show processes in container |
| `docker port container_id` | Show port mappings |
| `docker diff container_id` | Show filesystem changes |

## Docker Compose

### Basic Operations

| Command | Description |
|---------|-------------|
| `docker compose up` | Start services (Compose V2) |
| `docker compose up -d` | Start in detached mode |
| `docker compose up --build` | Build and start |
| `docker compose up --force-recreate` | Force recreate containers |
| `docker compose up --no-deps service` | Start service without dependencies |
| `docker compose down` | Stop and remove containers |
| `docker compose down -v` | Stop and remove volumes |
| `docker compose down --remove-orphans` | Remove orphaned containers |
| `docker compose start` | Start existing containers |
| `docker compose stop` | Stop running containers |
| `docker compose restart` | Restart services |
| `docker compose pause service` | Pause specific service |
| `docker compose unpause service` | Unpause specific service |

### Service Management

| Command | Description |
|---------|-------------|
| `docker compose ps` | List containers |
| `docker compose ps -a` | List all containers |
| `docker compose ls` | List compose projects |
| `docker compose logs` | Show logs for all services |
| `docker compose logs -f service_name` | Follow logs for service |
| `docker compose logs --tail=100 service_name` | Show last 100 lines |
| `docker compose exec service_name command` | Execute command in service |
| `docker compose exec -T service_name command` | Execute without TTY |
| `docker compose run service_name command` | Run one-time command |
| `docker compose run --rm service_name command` | Run and remove |
| `docker compose build` | Build services |
| `docker compose build --no-cache` | Build without cache |
| `docker compose build --parallel` | Build in parallel |
| `docker compose pull` | Pull service images |
| `docker compose push` | Push service images |
| `docker compose config` | Validate and view configuration |
| `docker compose config --profiles` | Show available profiles |

### Scaling & Profiles

| Command | Description |
|---------|-------------|
| `docker compose up --scale service=3` | Scale service to 3 instances |
| `docker compose --profile prod up` | Use specific profile |
| `docker compose -f docker-compose.yml -f docker-compose.prod.yml up` | Multiple files |
| `docker compose --env-file .env.prod up` | Use custom env file |
| `docker compose --project-name myproject up` | Set project name |

## Docker Buildx

| Command | Description |
|---------|-------------|
| `docker buildx version` | Show buildx version |
| `docker buildx ls` | List builders |
| `docker buildx create --name mybuilder` | Create builder |
| `docker buildx create --name mybuilder --driver docker-container` | Create with driver |
| `docker buildx use mybuilder` | Switch to builder |
| `docker buildx inspect mybuilder` | Inspect builder |
| `docker buildx rm mybuilder` | Remove builder |
| `docker buildx build --platform linux/amd64,linux/arm64 -t image .` | Multi-platform build |
| `docker buildx build --push --platform linux/amd64,linux/arm64 -t image .` | Build and push |
| `docker buildx build --load -t image .` | Build and load locally |
| `docker buildx build --output type=docker,dest=image.tar .` | Export to tar |
| `docker buildx bake` | Build from bake file |
| `docker buildx imagetools inspect image:tag` | Inspect remote image |

## Docker Init

| Command | Description |
|---------|-------------|
| `docker init` | Initialize Docker assets in project |
| `docker init --template node` | Initialize with specific template |
| `docker init --template go` | Initialize for Go project |
| `docker init --template python` | Initialize for Python project |

## Docker Scout

| Command | Description |
|---------|-------------|
| `docker scout quickview` | Quick vulnerability overview |
| `docker scout cves image:tag` | Show CVEs for image |
| `docker scout recommendations image:tag` | Get security recommendations |
| `docker scout compare image1:tag image2:tag` | Compare images |
| `docker scout sbom image:tag` | Generate SBOM |

## Docker Networking

| Command | Description |
|---------|-------------|
| `docker network ls` | List networks |
| `docker network create network_name` | Create bridge network |
| `docker network create --driver overlay network_name` | Create overlay network |
| `docker network create --driver macvlan network_name` | Create macvlan network |
| `docker network create --subnet=192.168.1.0/24 network_name` | Create with subnet |
| `docker network rm network_name` | Remove network |
| `docker network inspect network_name` | Inspect network |
| `docker network connect network container` | Connect container to network |
| `docker network connect --ip 192.168.1.10 network container` | Connect with IP |
| `docker network disconnect network container` | Disconnect from network |
| `docker run --network=network_name image` | Run in specific network |
| `docker run --network=host image` | Use host networking |
| `docker run --network=none image` | No networking |
| `docker network prune` | Remove unused networks |

## Docker Volumes

| Command | Description |
|---------|-------------|
| `docker volume ls` | List volumes |
| `docker volume create volume_name` | Create volume |
| `docker volume create --driver local volume_name` | Create with driver |
| `docker volume rm volume_name` | Remove volume |
| `docker volume inspect volume_name` | Inspect volume |
| `docker volume prune` | Remove unused volumes |
| `docker run -v volume_name:/path image` | Use named volume |
| `docker run -v /host/path:/container/path image` | Bind mount |
| `docker run -v /host/path:/container/path:ro image` | Read-only bind mount |
| `docker run --mount type=volume,src=vol,dst=/path image` | Mount syntax |
| `docker run --mount type=bind,src=/host,dst=/container image` | Bind mount syntax |
| `docker run --tmpfs /tmp image` | Tmpfs mount |

## Logging & Monitoring

### Container Logs

| Command | Description |
|---------|-------------|
| `docker logs container_id` | Show container logs |
| `docker logs -f container_id` | Follow logs |
| `docker logs --tail 100 container_id` | Show last 100 lines |
| `docker logs --since 1h container_id` | Show logs from last hour |
| `docker logs --until 2023-01-01 container_id` | Show logs until date |
| `docker logs -t container_id` | Show timestamps |
| `docker logs --details container_id` | Show extra details |

### System Monitoring

| Command | Description |
|---------|-------------|
| `docker stats` | Live container resource usage |
| `docker stats --no-stream` | Get one-time stats |
| `docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}"` | Format stats |
| `docker system df` | Show disk usage |
| `docker system df -v` | Verbose disk usage |
| `docker system events` | Show real-time events |
| `docker system events --filter container=mycontainer` | Filter events |
| `docker events --since 1h` | Events from last hour |

## Cleanup & Maintenance

### System Cleanup

| Command | Description |
|---------|-------------|
| `docker system prune` | Remove unused data |
| `docker system prune -a` | Remove all unused data |
| `docker system prune -a --volumes` | Include volumes |
| `docker system prune --filter="until=24h"` | Remove data older than 24h |
| `docker container prune` | Remove stopped containers |
| `docker container prune --filter="until=1h"` | Remove containers stopped 1h+ ago |
| `docker image prune` | Remove unused images |
| `docker image prune -a` | Remove all unused images |
| `docker volume prune` | Remove unused volumes |
| `docker volume prune --filter="label!=keep"` | Remove volumes without keep label |
| `docker network prune` | Remove unused networks |

### Bulk Operations

| Command | Description |
|---------|-------------|
| `docker stop $(docker ps -q)` | Stop all running containers |
| `docker rm $(docker ps -aq)` | Remove all containers |
| `docker rmi $(docker images -q)` | Remove all images |
| `docker kill $(docker ps -q)` | Kill all running containers |

## Production Best Practices

### Security

| Command | Description |
|---------|-------------|
| `docker run --user 1000:1000 image` | Run as non-root user |
| `docker run --read-only image` | Read-only filesystem |
| `docker run --security-opt=no-new-privileges image` | Disable privilege escalation |
| `docker run --cap-drop=ALL --cap-add=NET_BIND_SERVICE image` | Fine-tune capabilities |
| `docker run --security-opt seccomp=seccomp.json image` | Custom seccomp profile |
| `docker run --security-opt apparmor=docker-default image` | Use AppArmor |
| `docker scout cves image:tag` | Scan for vulnerabilities |

### Resource Management

| Command | Description |
|---------|-------------|
| `docker run --memory=512m image` | Set memory limit |
| `docker run --memory=1g --memory-swap=2g image` | Set memory and swap |
| `docker run --cpus=0.5 image` | Limit CPU usage |
| `docker run --cpuset-cpus=0,1 image` | Pin to specific CPUs |
| `docker run --oom-kill-disable image` | Disable OOM killer |
| `docker run --pids-limit=100 image` | Limit number of PIDs |
| `docker update --memory=1g container_id` | Update container resources |
| `docker update --restart=unless-stopped container_id` | Update restart policy |

### Health Checks

| Command | Description |
|---------|-------------|
| `docker run --health-cmd="curl -f http://localhost" image` | Add health check |
| `docker run --health-interval=30s --health-timeout=3s image` | Configure timing |
| `docker run --health-retries=3 image` | Set retry count |
| `docker run --health-start-period=60s image` | Grace period |
| `docker inspect --format='{{.State.Health.Status}}' container_id` | Check health status |

### Production Deployment

| Command | Description |
|---------|-------------|
| `docker run -d --restart=unless-stopped image` | Production restart policy |
| `docker run --log-driver=json-file --log-opt max-size=10m image` | Configure logging |
| `docker run --log-opt max-file=3 image` | Log rotation |
| `docker run --log-driver=syslog --log-opt syslog-address=tcp://host:514 image` | Remote logging |

## Advanced Commands

### Docker Context

| Command | Description |
|---------|-------------|
| `docker context ls` | List contexts |
| `docker context create mycontext --docker host=tcp://host:2376` | Create context |
| `docker context use mycontext` | Switch context |
| `docker context inspect mycontext` | Inspect context |
| `docker context rm mycontext` | Remove context |

### Docker Swarm

| Command | Description |
|---------|-------------|
| `docker swarm init` | Initialize swarm |
| `docker swarm join --token TOKEN HOST:PORT` | Join swarm |
| `docker node ls` | List swarm nodes |
| `docker service create --name web nginx` | Create service |
| `docker service ls` | List services |
| `docker service scale web=3` | Scale service |
| `docker service update --image nginx:latest web` | Update service |
| `docker secret create mysecret secret.txt` | Create secret |
| `docker config create myconfig config.txt` | Create config |

### Registry Operations

| Command | Description |
|---------|-------------|
| `docker save -o image.tar image:tag` | Save image to tar |
| `docker save image:tag \| gzip > image.tar.gz` | Save and compress |
| `docker load -i image.tar` | Load image from tar |
| `docker export container_id > container.tar` | Export container |
| `docker import container.tar new_image:tag` | Import container as image |

## Common Docker Patterns

### Development Environment

```bash
# Run with volume mounting for development
docker run -it --rm -v $(pwd):/app -w /app node:20 npm run dev

# Database with persistent storage and init scripts
docker run -d --name postgres \
  -e POSTGRES_PASSWORD=password \
  -v pgdata:/var/lib/postgresql/data \
  -v ./init.sql:/docker-entrypoint-initdb.d/init.sql \
  postgres:16
```

### Production Environment

```bash
# Production container with comprehensive configuration
docker run -d \
  --name app \
  --restart=unless-stopped \
  --health-cmd="curl -f http://localhost:3000/health || exit 1" \
  --health-interval=30s \
  --health-retries=3 \
  --health-timeout=10s \
  --health-start-period=60s \
  --memory=1g \
  --cpus=0.5 \
  --user=1000:1000 \
  --read-only \
  --tmpfs /tmp \
  --security-opt=no-new-privileges \
  -p 80:3000 \
  --log-driver=json-file \
  --log-opt max-size=10m \
  --log-opt max-file=3 \
  myapp:latest
```

### Multi-stage Dockerfile Example

```dockerfile
# syntax=docker/dockerfile:1
FROM node:20-alpine AS base
WORKDIR /app
COPY package*.json ./

FROM base AS deps
RUN npm ci --only=production

FROM base AS build
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine AS runtime
WORKDIR /app
RUN addgroup -g 1001 -S nodejs && adduser -S nextjs -u 1001
COPY --from=deps --chown=nextjs:nodejs /app/node_modules ./node_modules
COPY --from=build --chown=nextjs:nodejs /app/dist ./dist
USER nextjs
EXPOSE 3000
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1
CMD ["node", "dist/index.js"]
```

---

**Pro Tips:**

- Always use specific image tags instead of `latest` in production
- Use `.dockerignore` to exclude unnecessary files from build context
- Implement proper health checks for production containers
- Use multi-stage builds to reduce final image size
- Never store secrets in images; use Docker secrets or environment variables
- Regularly update base images for security patches
- Use `docker system prune` regularly to clean up unused resources
- Leverage multi-platform builds for cross-architecture compatibility
- Enable BuildKit for faster builds and advanced features
- Use init processes to handle zombie processes properly
- Implement proper logging strategies with log rotation
- Use read-only filesystems when possible for security
- Pin specific versions of dependencies in Dockerfiles
- Use non-root users in containers for better security
- Scan images regularly for vulnerabilities
