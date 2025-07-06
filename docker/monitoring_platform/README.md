# Monitoring Platform Configuration

Monitor! Monitor! Monitor! This is the config for my monitoring platform stack using InfluxDB and Grafana for visualization.

This config is so, so broken because there's nothing feeding it yet. Truth be told, I haven't spent enough time to onboard data sources in here yet. _coming soon tm_ 🤷‍♀️

## 1. Services Overview

### 1.1 [InfluxDB](https://github.com/influxdata/influxdb)

- **Image**: `influxdb:latest`
- **Purpose**: Time-series database for storing metrics and monitoring data.
- **Port**: `8086:8086` - Database API and web interface accessible at `http://localhost:8086`

### 1.2 [Grafana](https://github.com/grafana/grafana)

- **Image**: `grafana/grafana-oss:latest`
- **Purpose**: Data visualization and monitoring dashboards for metrics.
- **Port**: `3481:3000` - Web interface accessible at `http://localhost:3481`

## 2. Port Mappings

| Port | Service | Purpose |
|------|---------|---------|
| 8086 | InfluxDB | Database API and web interface |
| 3481 | Grafana | Dashboard web interface |

## 3. Environment Variables

Create a `.env` file in this directory with the following variables:

```bash
# Volume Configuration
VOLUME_LOCATION=/path/to/your/storage

# InfluxDB Configuration
INFLUXDB_DATABASE=your_database_name
INFLUXDB_USERNAME=your_influxdb_admin_user
INFLUXDB_PASSWORD=your_influxdb_admin_password
INFLUXDB_TOKEN=your_influxdb_token
INFLUXDB_ORG=your_influxdb_organization

# Grafana Configuration
GRAFANA_USERNAME=your_grafana_admin_user
GRAFANA_PASSWORD=your_grafana_admin_password
```

## 4. Volume Mounts

- **InfluxDB Data**: `${VOLUME_LOCATION}/monitoring_platform/influxdb:/var/lib/influxdb` - Database storage
- **Grafana Storage**: `${VOLUME_LOCATION}/monitoring_platform/grafana-storage:/var/lib/grafana` - Grafana configuration and data
- **Grafana Dashboards**: `${VOLUME_LOCATION}/monitoring_platform/grafana-dashboards/:/var/lib/grafana/dashboards/` - Pre-configured dashboards

## 5. Notes

- **Service Dependencies**: Grafana depends on InfluxDB and will wait for it to start.
- **Authentication**: Both services require admin credentials configured via environment variables.
- **Data Source**: Grafana is pre-configured to connect to the InfluxDB instance.