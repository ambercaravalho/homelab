# Plex Support Configuration

Media acquisition and management stack! These containers work together to automatically download and organize content for [Plex Media Server](/macos/plex/README.md).

_For educational purposes and backing up your legally owned media collection, of course._ 😉

## 1. Services Overview

### 1.1 [qBittorrent](https://github.com/qbittorrent/qBittorrent)

- **Image**: `ghcr.io/linuxserver/qbittorrent`
- **Purpose**: BitTorrent client for downloading content through the VPN tunnel.
- **Network**: Routes through `protonvpn` container for privacy protection.

### 1.2 [Bazarr](https://github.com/morpheus65535/bazarr)

- **Image**: `ghcr.io/hotio/bazarr:latest`
- **Purpose**: Subtitle management for movies and TV shows.
- **Network**: Routes through `protonvpn` container for indexer access.

### 1.3 [Lidarr](https://github.com/Lidarr/Lidarr)

- **Image**: `ghcr.io/hotio/lidarr:latest`
- **Purpose**: Music collection manager for automated album downloads and organization.
- **Network**: Routes through `protonvpn` container for indexer access.

### 1.4 [Prowlarr](https://github.com/Prowlarr/Prowlarr)

- **Image**: `ghcr.io/hotio/prowlarr`
- **Purpose**: Indexer manager that provides search results to all *arr applications.
- **Network**: Routes through `protonvpn` container for secure indexer access.

### 1.5 [Radarr](https://github.com/Radarr/Radarr)

- **Image**: `ghcr.io/hotio/radarr:latest`
- **Purpose**: Movie collection manager for automated movie downloads and organization.
- **Network**: Routes through `protonvpn` container for indexer access.

### 1.6 [Sonarr](https://github.com/Sonarr/Sonarr)

- **Image**: `ghcr.io/hotio/sonarr:latest`
- **Purpose**: TV series collection manager for automated episode downloads and organization.
- **Network**: Routes through `protonvpn` container for indexer access.

### 1.7 [FlareSolverr](https://github.com/FlareSolverr/FlareSolverr)

- **Image**: `ghcr.io/flaresolverr/flaresolverr:latest`
- **Purpose**: Cloudflare anti-bot bypass service for accessing protected indexers.
- **Network**: Routes through `protonvpn` container alongside other services.

## 2. Port Mappings

All services route through the VPN gateway container (`protonvpn`) on the [external_access](/docker/external_access/README.md) stack. Ports are exposed via the external access configuration:

| Port | Service | Purpose |
|------|---------|---------|
| 6011 | qBittorrent | Torrent client web interface |
| 7878 | Radarr | Movie management web interface |
| 8989 | Sonarr | TV series management web interface |
| 8686 | Lidarr | Music management web interface |
| 6767 | Bazarr | Subtitle management web interface |
| 9696 | Prowlarr | Indexer management web interface |
| 8191 | FlareSolverr | Anti-bot bypass service |

## 3. Environment Variables

Create a `.env` file in this directory with the following variables:

```bash
# Volume Configuration
VOLUME_LOCATION=/path/to/your/storage
PLEX_MEDIA_LIBRARY=/path/to/your/plex/media

# FlareSolverr Configuration (optional)
LOG_LEVEL=info
LOG_HTML=false
CAPTCHA_SOLVER=none
```

## 4. Volume Mounts

### 4.1 Application Data

- **qBittorrent**: `${VOLUME_LOCATION}/plex_support/qbittorrent:/config` - Client configuration
- **Bazarr**: `${VOLUME_LOCATION}/plex_support/bazarr:/config` - Subtitle manager config
- **Lidarr**: `${VOLUME_LOCATION}/plex_support/lidarr:/config` - Music manager config
- **Prowlarr**: `${VOLUME_LOCATION}/plex_support/prowlarr:/config` - Indexer manager config
- **Radarr**: `${VOLUME_LOCATION}/plex_support/radarr:/config` - Movie manager config
- **Sonarr**: `${VOLUME_LOCATION}/plex_support/sonarr:/config` - TV manager config

### 4.2 Media Storage

- **Torrent Downloads**: `${PLEX_MEDIA_LIBRARY}/shared_data/torrents:/data/torrents` - Download destination
- **Media Library**: `${PLEX_MEDIA_LIBRARY}/shared_data:/data` - Organized media storage

## 5. Other Things

1. **VPN Dependency**: All services depend on the `gluetun` VPN container from external access configuration
2. **Network Isolation**: Services use `container:protonvpn` network mode for privacy

## 6. Notes

- **VPN Routing**: All traffic from these services routes through the VPN for privacy \*purposes*\.
- **Service Dependencies**: All services wait for the VPN gateway to start before launching.
- **User Permissions**: Services run as root (PUID=0, PGID=0) for file system access.
- **Integration**: Prowlarr provides indexers to all *arr applications automatically.