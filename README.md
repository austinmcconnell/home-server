# Home Server

This repository contains Docker Compose configurations for running various services on a home server.

## Deployment

This configuration is designed to be platform-agnostic and can be deployed on any system running Docker.

### Current Deployment

These services are currently running on a Synology NAS. To manage the services from a development machine:

```bash
# Set the Docker context to the remote host
docker context use hoid-is-my-hero

# Now docker compose commands will execute on the remote host
docker compose up -d
```

## Docker Configuration

### Structure

The repository is organized with a modular approach:

- Each service has its own directory containing a dedicated `docker-compose.yaml` file
- Services can be managed individually or in groups as needed

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

#### Running Multiple Services

To manage multiple services, you can use shell commands:

```bash
# Start all services
for service in duplicati portainer pi-hole home-assistant plex; do
  cd $service && docker compose up -d && cd ..
done
```

### Dependencies

Services have dependencies on each other's volumes. For example:

- Duplicati backs up volumes from Home Assistant, Pi-hole, and Portainer
- These dependencies are managed through external volume references

### Requirements

- Docker Engine 20.10.0+
- Docker Compose v2.0.0+
