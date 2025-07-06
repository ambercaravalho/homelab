# Internal Services Configuration

Docker services for managing internal operations, including container monitoring, automation, and dashboard interfaces.

## 1. Services Overview

### 1.1 [Autoheal](https://github.com/willfarrell/docker-autoheal)

- **Image**: `tmknight88/docker-autoheal:latest`
- **Purpose**: Restarts unhealthy containers based on health checks.
- **Security**: Read-only filesystem with socket access for container management.

### 1.2 [Glance Dashboard](https://github.com/glanceapp/glance)

- **Image**: `glanceapp/glance`
- **Purpose**: A clean, customizable dashboard for monitoring services. _so pretty! 🤩_
- **Port**: `2811:8080` - Web interface accessible at `http://localhost:2811`

### 1.3 [Homebridge](https://github.com/homebridge/homebridge)

- **Image**: `homebridge/homebridge:latest`
- **Purpose**: Bridges non-HomeKit devices to Apple's stupid (but secure) walled garden.
- **Network**: Host networking for device discovery and communication.

### 1.4 [Portainer](https://github.com/portainer/portainer)

- **Image**: `portainer/portainer-ce:latest`
- **Purpose**: Web-based Docker management interface.
- **Port**: `7328:9000` - Management UI accessible at `http://localhost:7328`

### 1.5 [Watchtower](https://github.com/containrrr/watchtower)

- **Image**: `containrrr/watchtower`
- **Purpose**: Updates Docker containers to latest versions.
- **Security**: Read-only filesystem with socket access for container management.

## 2. Port Mappings

| Port | Service | Purpose |
|------|---------|---------|
| 2811 | Glance | Dashboard web interface |
| 7328 | Portainer | Docker management UI |
| 8080 | Homebridge | Uses host networking |
| N/A | Autoheal | No network exposure |
| N/A | Watchtower | No network exposure |

## 3. Environment Variables

Create a `.env` file in this directory with the following variables:

```bash
# Volume Configuration
VOLUME_LOCATION=/path/to/your/storage
```

## 4. Volume Mounts

### 4.1 Data Persistence

- **Autoheal**: `${VOLUME_LOCATION}/internal_services/autoheal/log.json` - Persistent logging
- **Glance**: `${VOLUME_LOCATION}/internal_services/glance` - Dashboard configuration
- **Homebridge**: `${VOLUME_LOCATION}/internal_services/homebridge` - HomeKit bridge config
- **Portainer**: `${VOLUME_LOCATION}/internal_services/portainer` - Management data

### 4.2 Docker Socket Access

Multiple services require Docker socket access for container management:

- Autoheal (read-only) - Monitor container health
- Glance (read-only) - Display container status
- Portainer (read-write) - Full container management
- Watchtower (read-write) - Update containers

## 5. Notes

- **Security**: Autoheal runs as root but with read-only filesystem for security.
- **Networking**: Homebridge uses host networking for device discovery.
- **Updates**: Watchtower will automatically update containers (configure schedule as needed).
- **Health Monitoring**: Autoheal only works with containers that have proper health checks.
