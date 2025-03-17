# MSSQL Docker Setup

This project contains Docker configuration for running Microsoft SQL Server in a container.

## Quick Start

1. Start the container:
```bash
docker-compose up -d
```

2. Connect to SQL Server:
- Server: localhost,1433
- User: sa
- Password: YourStrong@Passw0rd

## Environment Variables

Key environment variables used in this setup:

| Variable | Description | Value |
|----------|-------------|--------|
| ACCEPT_EULA | Accept the End-User License Agreement | Y |
| SA_PASSWORD | System Administrator (SA) password | YourStrong@Passw0rd |
| MSSQL_PID | SQL Server Edition | Developer (default) |

## Container Details

- Image: mcr.microsoft.com/mssql/server:2019-latest
- Port: 1433
- Persistent Storage: Volume mounted at /var/opt/mssql

## Requirements

- Docker
- Docker Compose
- Minimum 2GB of RAM allocated to Docker

## Common Commands

```bash
# Start container
docker-compose up -d

# Stop container
docker-compose down

# View logs
docker-compose logs mssql

# Connect to container
docker exec -it mssql_server /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P YourStrong@Passw0rd
```

## Notes

- The SQL Server data is persisted using Docker volumes
- Container automatically restarts unless manually stopped
- Default port 1433 must be available on host machine