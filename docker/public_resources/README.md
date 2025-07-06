# Public Resources Configuration

HMU on the open World Wide Web! These containers provide various tools and archived websites accessible through my Cloudflare Zero Trust.

## 1. Services Overview

### 1.1 [Open WebUI](https://github.com/open-webui/open-webui)

- **Image**: `ghcr.io/open-webui/open-webui:main`
- **Purpose**: Web interface for interacting with local LLM models and AI services.
- **Port**: `3000:8080` - Web interface accessible at `http://localhost:3000`

### 1.2 [Planning Poker](https://github.com/axeleroy/self-host-planning-poker)

- **Image**: `axeleroy/self-host-planning-poker:latest`
- **Purpose**: Self-hosted planning poker application for agile estimation sessions.
- **Port**: `4222:8000` - Web interface accessible at `http://localhost:4222`

### 1.3 [WordPress Archive v2](https://github.com/bitnami/bitnami-docker-wordpress)

- **Image**: `docker.io/bitnami/wordpress:latest`
- **Purpose**: WordPress instance for archived website content.
- **Port**: `3842:80` - Web interface accessible at `http://localhost:3840`

### 1.4 [WordPress Archive v3](https://hub.docker.com/_/wordpress)

- **Image**: `wordpress:latest`
- **Purpose**: Standard WordPress instance for archived website content.
- **Port**: `3838:80` - Web interface accessible at `http://localhost:3838`

### 1.5 [WordPress Cyber Games](https://hub.docker.com/_/wordpress)

- **Image**: `wordpress:latest`
- **Purpose**: WordPress instance for archived cyber games website content.
- **Port**: `3840:80` - Web interface accessible at `http://localhost:3840`

## 2. Port Mappings

| Port | Service | Purpose |
|------|---------|---------|
| 3000 | Open WebUI | AI/LLM web interface |
| 4222 | Planning Poker | Agile estimation tool |
| 3842 | WordPress v2 | Archived website v2 |
| 3838 | WordPress v3 | Archived website v3 |
| 3840 | WordPress Cyber Games | Archived cyber games site |

## 3. Environment Variables

Create a `.env` file in this directory with the following variables:

```bash
# Volume Configuration
VOLUME_LOCATION=/path/to/your/storage

# WordPress Archive v2 Database
WORDPRESS_DATABASE_USER_ARCHIVE_V2=wp_user_v2
WORDPRESS_DATABASE_NAME_ARCHIVE_V2=wordpress_v2
WORDPRESS_DATABASE_PASSWORD_ARCHIVE_V2=your_secure_password_v2

# WordPress Archive v3 Database
WORDPRESS_DATABASE_USER_ARCHIVE_V3=wp_user_v3
WORDPRESS_DATABASE_NAME_ARCHIVE_V3=wordpress_v3
WORDPRESS_DATABASE_PASSWORD_ARCHIVE_V3=your_secure_password_v3

# WordPress Cyber Games Database
WORDPRESS_DATABASE_USER_ARCHIVE_JBLECYBERGAMES=wp_user_cyber
WORDPRESS_DATABASE_NAME_ARCHIVE_JBLECYBERGAMES=wordpress_cyber
WORDPRESS_DATABASE_PASSWORD_ARCHIVE_JBLECYBERGAMES=your_secure_password_cyber
```

## 4. Volume Mounts

### 4.1 Application Data

- **Open WebUI**: `${VOLUME_LOCATION}/public_resources/open-webui:/app/backend/data` - Application data and configurations
- **Planning Poker**: `${VOLUME_LOCATION}/public_resources/planning-poker/data:/data` - Application data

### 4.2 Planning Poker Customization

- **App Icon**: `${VOLUME_LOCATION}/public_resources/planning-poker/customization/app-icon.svg:/app/static/assets/icon.svg`
- **Favicon**: `${VOLUME_LOCATION}/public_resources/planning-poker/customization/favicon-package:/app/static/assets/favicon`
- **CSS Overrides**: `${VOLUME_LOCATION}/public_resources/planning-poker/customization/overrides.css:/app/static/overrides.css`

### 4.3 WordPress Data

- **WordPress v2**: `${VOLUME_LOCATION}/public_resources/archive-v2-wordpress/wp-data:/bitnami/wordpress` - Bitnami WordPress data
- **WordPress v2 DB**: `${VOLUME_LOCATION}/public_resources/archive-v2-wordpress/db:/bitnami/mariadb` - MariaDB data
- **WordPress v3**: `${VOLUME_LOCATION}/public_resources/archive-v3_wordpress:/var/www/html` - Standard WordPress data
- **WordPress v3 DB**: `${VOLUME_LOCATION}/public_resources/archive-v3_wordpress/db:/var/lib/mysql` - MySQL data
- **WordPress Cyber**: `${VOLUME_LOCATION}/public_resources/cyber-games_wordpress:/var/www/html` - Cyber games WordPress data
- **WordPress Cyber DB**: `${VOLUME_LOCATION}/public_resources/cyber-games_wordpress/db:/var/lib/mysql` - MySQL data

## 5. Other Things

1. **Network Dependencies**: Create required WordPress networks before starting:

   ```bash
   docker network create wordpress_db_archive_v2
   docker network create wordpress_db_archive_v3
   docker network create wordpress_db_archive_cybergames
   docker network create cloudflared
   ```

3. **External Access**: All services are connected to the `cloudflared` network for secure public access.

## 6. Notes

- **Database Isolation**: Each WordPress instance has its own dedicated database container and network.
- **Custom Branding**: Planning Poker supports extensive customization through volume mounts.
- **Security**: Database containers **SHOULD** use random root passwords for enhanced security.