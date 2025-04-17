# Home Server

This repository contains Docker Compose configurations for running various services on a home server.

## Docker Configuration

### Structure

The repository is organized with a modular approach:

- Each service has its own directory containing a dedicated `docker-compose.yaml` file
- A master `docker-compose.yaml` file in the root directory uses the `include` directive to
  combine all services

### Services

- **Duplicati**: Backup solution for protecting your data
- **Home Assistant**: Home automation platform
- **Pi-hole**: Network-wide ad blocking and DNS server
- **Portainer**: Container management UI
- **Wireguard**: VPN server
- **Wireshark**: Network protocol analyzer

### Volume Naming Convention

All volumes are explicitly named to ensure consistency regardless of which docker-compose file is used:

- `duplicati_backups`, `duplicati_config`, `duplicati_source`
- `home-assistant_config`
- `pi-hole_dnsmasq`, `pi-hole_pihole`
- `portainer_data`, `portainer_portainer`

### Usage

#### Running Individual Services

You can start, stop, or manage individual services:

```bash
cd duplicati
docker compose up -d
```

#### Running All Services

To manage all services at once, use the master docker-compose file:

```bash
# From the repository root
docker compose up -d
```

### Dependencies

Services have dependencies on each other's volumes. For example:

- Duplicati backs up volumes from Home Assistant, Pi-hole, and Portainer
- These dependencies are managed through external volume references

### Requirements

- Docker Engine 20.10.0+
- Docker Compose v2.20.0+ (for the `include` directive)
