# homelab

My personal HomeLab configuration. A collection of scripts, configs, and container orchestration for running services on macOS.

_This repo will likely always be in progress and should never be taken seriously._ 🏠

> Will things work in your environment? Will I ever start using proper CI/CD pipelines? Will I accidentally expose a secret here eventually? _Who knows?!_ That's the fun of it.

## 1. Configuration Categories

### 1.1 [macOS Setup](/macos/README.md)
- **Purpose**: Base system configuration for running containers on macOS
- **Includes**: Brew packages, Colima setup, system settings, and essential services
- **Priority**: Complete this first before deploying any containers

### 1.2 [Docker Services](/docker/README.md)
- **Purpose**: Container orchestration for various homelab services
- **Includes**: Media management, monitoring, external access, and productivity tools
- **Stack**: Standalone Docker Compose (because complexity is overrated)

## 2. Quick Start

1. **System Setup**: Follow the [macOS configuration guide](/macos/README.md) first.
2. **Service Deployment**: Choose and deploy [Docker services](/docker/README.md) as needed.
3. **Enjoy**: Watch containers do the work while you pretend to understand networking.

## 3. Notes

- **Security**: This is a homelab, not production - adjust security accordingly.
- **Compatibility**: Designed for macOS but principles apply to other systems.
- **Support**: Documentation is provided as-is with sarcasm included.

_"life is pain when you refuse to use proper server operating systems"_ - Alan Turing (probably)