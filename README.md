# Portainer Docker Setup

This repository contains a Docker Compose configuration for running Portainer CE (Community Edition), a lightweight management UI for Docker environments.

## What is Portainer?

Portainer is a web-based Docker management interface that allows you to easily manage your Docker containers, images, networks, and volumes through an intuitive web UI.

## Prerequisites

- Docker Engine installed on your system
- Docker Compose installed on your system

## Quick Start

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd portainer
   ```

2. Start Portainer:
   ```bash
   docker-compose up -d
   ```

3. Access Portainer in your web browser:
   ```
   http://localhost:9000
   ```

4. On first access, you'll be prompted to create an admin user account.

## Configuration

The `docker-compose.yml` file includes the following configuration:

- **Image**: `portainer/portainer-ce:latest` - The latest Portainer Community Edition
- **Port**: `9000` - Web interface accessible on port 9000
- **Volumes**: 
  - `/var/run/docker.sock:/var/run/docker.sock` - Allows Portainer to communicate with Docker
  - `portainer_data:/data` - Persistent storage for Portainer data
- **Restart Policy**: `always` - Automatically restarts the container if it stops

## Usage

### Starting Portainer
```bash
docker-compose up -d
```

### Stopping Portainer
```bash
docker-compose down
```

### Viewing Logs
```bash
docker-compose logs portainer
```

### Updating Portainer
```bash
docker-compose pull
docker-compose up -d
```

## Security Considerations

- Change the default port (9000) if needed for security reasons
- Consider setting up SSL/TLS for production environments
- Restrict access to the Portainer interface using firewalls or reverse proxies
- Regularly update to the latest version for security patches

## Troubleshooting

### Port Already in Use
If port 9000 is already in use, modify the port mapping in `docker-compose.yml`:
```yaml
ports:
  - "8080:9000"  # Change 9000 to any available port
```

### Permission Issues
Ensure the Docker socket has proper permissions:
```bash
sudo chmod 666 /var/run/docker.sock
```

## Data Persistence

Portainer data is stored in a Docker volume named `portainer_data`. This ensures that your settings, users, and configurations persist across container restarts.

To backup Portainer data:
```bash
docker run --rm -v portainer_data:/data -v $(pwd):/backup alpine tar czf /backup/portainer-backup.tar.gz -C /data .
```

To restore Portainer data:
```bash
docker run --rm -v portainer_data:/data -v $(pwd):/backup alpine tar xzf /backup/portainer-backup.tar.gz -C /data
```

## Contributing

Feel free to submit issues and enhancement requests!

## License

This project is provided as-is. Portainer itself is licensed under the zlib License.