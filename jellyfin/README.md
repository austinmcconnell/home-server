# Jellyfin Media Server

Jellyfin is a free and open-source media server that provides a privacy-focused alternative to Plex.

## Features

- **100% Free and Open Source**: No premium features or subscriptions required
- **Privacy-Focused**: No telemetry, external accounts, or data collection
- **Self-Hosted**: Complete control over your media and metadata
- **Cross-Platform**: Supports all major devices and platforms including iOS, Apple TV,
  Android, and web browsers

## Configuration

### Ports

- **8096**: HTTP web interface and API
- **8920**: HTTPS web interface (if SSL is configured)
- **7359/udp**: Auto-discovery on local network
- **1900/udp**: DLNA discovery

### Volumes

- **Config**: `/config` - Jellyfin configuration, metadata, and database
- **Movies**: `/movies` - Read-only access to movie library (shared with Plex)
- **TV Shows**: `/tv` - Read-only access to TV show library (shared with Plex)

### Environment Variables

- **PUID/PGID**: User and group IDs for file permissions (1029/65537)
- **TZ**: Timezone set to US/Central
- **UMASK**: File creation mask (022)

## Access

Once running, Jellyfin will be available at:

- **Web Interface**: `http://your-server-ip:8096`
- **Setup Wizard**: First-time setup will guide you through initial
  configuration

## Initial Setup

1. Navigate to the web interface
1. Create an admin account
1. Add media libraries pointing to `/movies` and `/tv`
1. Configure metadata providers and other preferences
1. Install client apps on your devices

## Client Apps

- **iOS**: Jellyfin Mobile (free)
- **Apple TV**: Jellyfin for Apple TV (free)
- **Android**: Jellyfin for Android (free)
- **Web**: Any modern web browser
- **Desktop**: Jellyfin Media Player or web interface

## Backup

The Jellyfin configuration volume (`jellyfin_config`) is automatically backed up by
Duplicati along with other service configurations.
