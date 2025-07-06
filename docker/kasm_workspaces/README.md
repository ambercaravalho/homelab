# Kasm Workspaces Configuration

Kasm Workspaces is one of those really cool technologies that I probably _don't actually need_ to host. By whatever, a containerized streaming platform that runs completely on Docker? That's cool as hell.

## 1. Services Overview

### 1.1 [Kasm Workspaces](https://www.kasmweb.com/docs/latest/install/single_server_install.html)

- **Image**: `lscr.io/linuxserver/kasm:latest`
- **Purpose**: Provides streaming containerized desktop environments and applications. _browsers in browsers in browsers in browsers!_
- **Network**: Connected to `cloudflared` network for Cloudflare Access OAUTH.

## 2. Port Mappings

| Port | Service | Purpose |
|------|---------|---------|
| 3843 | Kasm Web UI | Alternative web interface access |
| 443 | Kasm HTTPS | Primary secure web interface |

## 3. Environment Variables

Create a `.env` file in this directory with the following variables:

```bash
# Volume Configuration
VOLUME_LOCATION=/path/to/your/storage
```

## 4. Volume Mounts

- **Kasm Data**: `${VOLUME_LOCATION}/kasm_workspaces/data:/opt` - Application data and configurations
- **User Profiles**: `${VOLUME_LOCATION}/kasm_workspaces/profiles:/profiles` - User workspace profiles and settings

## 5. Notes

- **Privileged Mode**: Required for container-in-container workspace isolation.
- **Resource Usage**: Can be resource-intensive depending on workspace count and types.
- **Storage**: User profiles and workspace data persist between container restarts.
- **Browser Compatibility**: Works best with modern browsers supporting WebRTC.