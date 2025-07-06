# Docker Configuration

Container orchestration for the homelab! Everything here runs on [standalone Docker Compose](https://docs.docker.com/compose/install/standalone/) because complexity is overrated.

_I swear I'll start migrating to [Docker Swarm](https://docs.docker.com/engine/swarm/) or [K8s](https://kubernetes.io/docs/home/) eventually, but that feels like a lot of work._ 🤷‍♀️

## Prerequisites

> ⚠️ **IMPORTANT**: For the love of all things, finish the [macOS Configuration](/macos/README.md) before touching this stuff!

## Services

- **[External Access](/docker/external_access/README.md)** - VPN routing and Cloudflare tunnels
- **[Internal Services](/docker/internal_services/README.md)** - Container monitoring and management tools
- **[Plex Support](/docker/plex_support/README.md)** - Media acquisition and organization stack
- **[Public Resources](/docker/public_resources/README.md)** - Web applications and archived sites
- **[Kasm Workspaces](/docker/kasm_workspaces/README.md)** - Containerized desktop environments
- **[Monitoring Platform](/docker/monitoring_platform/README.md)** - InfluxDB and Grafana metrics stack

"_senior engineers don't actually review code_" - the voices in my head