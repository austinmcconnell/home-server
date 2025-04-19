# Docker Compose Usage Guidelines

This document outlines strict rules for Amazon Q when interacting with Docker Compose in this repository.

## Prohibited Commands

Amazon Q MUST NEVER execute or suggest executing any of the following commands that change the state
of running Docker services:

- `docker compose up` (including with `-d` flag)
- `docker compose down`
- `docker compose start`
- `docker compose stop`
- `docker compose restart`
- `docker compose pull`
- `docker compose build`
- `docker compose create`
- `docker compose kill`
- `docker compose rm`
- `docker compose pause`
- `docker compose unpause`

## Allowed Commands

Amazon Q may only use Docker Compose commands that gather information without changing service state:

- `docker compose ps` - List containers
- `docker compose ls` - List running compose projects
- `docker compose config` - Validate and view compose configuration
- `docker compose images` - List images used by services
- `docker compose top` - Display running processes
- `docker compose logs` (read-only) - View service logs
- `docker compose port` - Print port mapping information
- `docker compose events` (read-only) - Receive real-time events

## Additional Docker Commands for Information Gathering

These Docker commands may also be used to gather information:

- `docker volume ls` - List volumes
- `docker network ls` - List networks
- `docker inspect` - Return detailed information on containers/images
- `docker stats` - Display container resource usage statistics

## Rationale

These restrictions are in place because:

1. The home server runs critical services that should not be disrupted
1. Service state changes should only be performed manually by the repository owner
1. Information gathering is sufficient for analysis and troubleshooting purposes

## Compliance

Amazon Q must strictly adhere to these guidelines. If a user requests execution of a prohibited
command, Amazon Q must:

1. Decline to execute the command
1. Explain that it cannot modify running service states
1. Suggest information-gathering alternatives if appropriate
