# Passbolt Setup with Docker Compose for Secure Team Password Management

This repository provides a comprehensive guide for setting up Passbolt, a secure, open-source password manager for teams. The configuration uses Docker Compose with Traefik to enable HTTPS, ensuring that passwords are safely managed and accessed across your organization.

### By the end of this setup, you’ll be able to:

- Deploy Passbolt using Docker Compose.
- Secure your Passbolt instance with Traefik as a reverse proxy with HTTPS.
- Configure user settings and create admin accounts for secure access.

## Prerequisites

To follow this guide, you’ll need:

- A Linux server or VM with a public IP.
- Docker Engine and Docker Compose installed.
- A domain name pointed to your server.
  
This tutorial was demonstrated using an Azure VM with the domain `passbolt.dev.softsweb.site`.

## Setup Guide

### 1. Directory and Docker Compose Setup

Create a working directory for Passbolt and configure the necessary Docker Compose file.

```bash
cd /opt
mkdir passbolt
cd passbolt
nano docker-compose.yml
```

### 2. Traefik Configuration

Ensure Traefik is running as an HTTPS reverse proxy. Set up the required configuration files in `/etc/traefik/`:

- `traefik.yaml`: Traefik configuration.
- `headers.yaml`: Middleware configuration for additional security headers.

### 3. Launch Passbolt

Start Passbolt and Traefik by creating the Docker network and launching the containers.

```bash
docker network create traefik
docker-compose up -d
```

### 4. Initial Admin User Creation
Use the following command to create an initial admin user:

```bash
docker compose exec passbolt su -m -c "/usr/share/php/passbolt/bin/cake passbolt register_user -u <your-email> -f <First-Name> -l <Last-Name> -r admin" -s /bin/sh www-data
```

### 5. Finalize the Setup
Open the setup link generated for the admin user and complete account creation, including setting a strong passphrase and downloading the recovery kit.

### Additional Configuration and Security Options
Explore Passbolt’s profile settings for secure access, sharing permissions, and customizations. Ensure your passphrase and private key are securely stored and not shared with anyone.

### Troubleshooting
If you encounter issues, check:

1. Domain configuration in DNS.
2. Docker and Traefik logs:

```
docker logs <container_id>
```

## Contributing
Feel free to open an issue or pull request for suggestions.

## Follow Me for More Tutorials!

YouTube: [SoftsWeb Channel](https://www.youtube.com/@SoftsWeb)

Website: [SoftsWeb](https://softsweb.com)

## License
This project is open source and available under the MIT License.
