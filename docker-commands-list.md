# Docker Commands Cheatsheet 🐳

## 🏗️ Build

```bash
docker build -t <name>:<tag> .                        # Build image
docker build -t myapp:1.0 .                           # With version tag
docker build -t myapp:latest --no-cache .             # Force rebuild (no cache)
docker build -f Dockerfile.prod -t myapp:prod .       # Custom Dockerfile
docker build --build-arg ENV=production -t myapp .    # Pass build args
```

---

## 🚀 Run Containers

```bash
docker run <image>                                    # Run container
docker run -d <image>                                 # Run in background (detached)
docker run -it <image> bash                           # Run with interactive terminal
docker run --name mycontainer <image>                 # Custom container name
docker run -p 8080:8080 <image>                       # Port mapping (host:container)
docker run -p 8080:8080 -d --name myapp myimage       # Full combo

# Environment variables
docker run -e "SPRING_PROFILES_ACTIVE=dev" <image>
docker run --env-file .env <image>                    # From .env file

# Volume mount
docker run -v /host/path:/container/path <image>
docker run -v $(pwd):/app <image>                     # Current dir mount

# Force remove when stopped
docker run --rm <image>                               # Auto cleanup
```

---

## 📋 Container Management

```bash
docker ps                        # Running containers
docker ps -a                     # All containers (stopped bhi)
docker ps -q                     # Only container IDs

docker stop <container>          # Graceful stop
docker start <container>         # Start stopped container
docker restart <container>       # Restart container
docker kill <container>          # Force kill ⚠️

docker rm <container>            # Remove stopped container
docker rm -f <container>         # Force remove running container ⚠️
docker rm $(docker ps -aq)       # Remove ALL containers ⚠️

docker logs <container>          # View logs
docker logs -f <container>       # Follow logs (live)
docker logs --tail 100 <container>  # Last 100 lines

docker exec -it <container> bash    # Enter running container
docker exec <container> <command>   # Run command in container
```

---

## 🖼️ Image Management

```bash
docker images                    # List all images
docker images -a                 # All images (intermediate bhi)

docker pull <image>:<tag>        # Pull from registry
docker push <image>:<tag>        # Push to registry

docker rmi <image>               # Remove image
docker rmi -f <image>            # Force remove image ⚠️
docker rmi $(docker images -q)   # Remove ALL images ⚠️

docker tag <image> <new-name>:<tag>   # Rename/retag image

# Image details
docker inspect <image>
docker history <image>           # Layer history
```

---

## 🧹 Cleanup (Prune)

```bash
docker system prune              # Remove unused: containers, networks, images
docker system prune -a           # Remove ALL unused including tagged images ⚠️
docker system prune --volumes    # Include volumes ⚠️

docker container prune           # Remove all stopped containers
docker image prune               # Remove dangling images
docker image prune -a            # Remove all unused images ⚠️
docker volume prune              # Remove unused volumes
docker network prune             # Remove unused networks

# Check disk usage
docker system df
```

---

## 🐙 Docker Compose

```bash
docker compose up                # Start services
docker compose up -d             # Start in background
docker compose up --build        # Rebuild before starting
docker compose up --force-recreate   # Force recreate containers

docker compose down              # Stop + remove containers
docker compose down -v           # Also remove volumes ⚠️
docker compose down --rmi all    # Also remove images ⚠️

docker compose ps                # List compose containers
docker compose logs              # View all logs
docker compose logs -f           # Follow logs
docker compose logs -f <service> # Follow specific service logs

docker compose restart           # Restart all services
docker compose restart <service> # Restart specific service

docker compose exec <service> bash   # Enter service container
docker compose build             # Build all services
docker compose build --no-cache  # Force rebuild ⚠️

docker compose pull              # Pull latest images
docker compose config            # Validate compose file
```

---

## 🌐 Networks

```bash
docker network ls                           # List networks
docker network create <name>               # Create network
docker network inspect <name>              # Network details
docker network rm <name>                   # Remove network

# Connect container to network
docker network connect <network> <container>
docker network disconnect <network> <container>
```

---

## 💾 Volumes

```bash
docker volume ls                 # List volumes
docker volume create <name>      # Create volume
docker volume inspect <name>     # Volume details
docker volume rm <name>          # Remove volume
docker volume prune              # Remove unused volumes ⚠️
```

---

## 🔍 Inspect & Debug

```bash
docker inspect <container/image>          # Full details (JSON)
docker stats                              # Live resource usage
docker stats <container>                  # Specific container stats
docker top <container>                    # Running processes inside
docker port <container>                   # Port mappings
docker diff <container>                   # Changed files in container
docker cp <container>:/path ./local       # Copy file from container
docker cp ./local <container>:/path       # Copy file to container
```

---

## ⚡ Power Combos

```bash
# Stop all running containers
docker stop $(docker ps -q)

# Remove all stopped containers
docker rm $(docker ps -aq)

# Full nuclear cleanup (sab kuch saaf) ⚠️
docker system prune -a --volumes

# See container IP address
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container>

# Export/Import image (without registry)
docker save myapp:latest > myapp.tar
docker load < myapp.tar
```
