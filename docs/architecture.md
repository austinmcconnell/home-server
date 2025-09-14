# Home Server Architecture

## Overview

This project implements a modular Docker Compose-based home server setup designed to run on any
Docker-capable system, currently deployed on a Synology NAS.

## Design Principles

1. **Modularity**: Each service has its own directory and configuration
1. **Consistency**: Standardized volume naming conventions
1. **Flexibility**: Services can be run individually or as a complete stack
1. **Portability**: Platform-agnostic design

## Component Architecture

```text
home-server/
├── duplicati/                # Backup service
│   └── docker-compose.yaml
├── home-assistant/           # Home automation platform
│   └── docker-compose.yaml
├── pi-hole/                  # Network-wide ad blocking
│   └── docker-compose.yaml
├── portainer/                # Container management
│   └── docker-compose.yaml
├── wireguard/                # VPN server
│   └── docker-compose.yaml
└── wireshark/                # Network protocol analyzer
    └── docker-compose.yaml
```

## Volume Dependencies

Duplicati backs up volumes from other services:

- home-assistant_config
- pi-hole_dnsmasq
- pi-hole_pihole
- portainer_data
- portainer_portainer

## Networking

Services are interconnected through Docker networks, with specific ports exposed as needed.

## Deployment Model

Remote management is facilitated through Docker contexts:

```bash
docker context use hoid-is-my-hero
```

## Naming Conventions

### Docker Volumes

All volumes follow the pattern: `{service_name}_{purpose}`

Examples:

- duplicati_backups
- home-assistant_config
- pi-hole_dnsmasq
