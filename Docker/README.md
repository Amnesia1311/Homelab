# Homelab Docker with Traefik and Wilcard certificates

The repository provides some containers in relation to Traefik as a reverse proxy.
The goal was to provide Traefik with wildcard certificates via lets encrypt and to achieve an A+ rating in [ssllabs](https://www.ssllabs.com/ssltest/).

## First Steps
1. Install Docker
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```
2. Change traefik config to your needs and spin up traefik
3. After this its possible to publish the other container