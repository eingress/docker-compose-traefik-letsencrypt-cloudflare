# Docker-Compose Traefik + Lets Encrypt + Cloudflare

  A docker compose configuration for spinning up a [Traefik v2](https://traefik.io/) instance with [Lets Encrypt DNS-01 challenge](https://letsencrypt.org/docs/challenge-types/#dns-01-challengw) supported through [Cloudflare](cloudflare.com).

## Usage

```sh
cp .env.dev .env # edit .env as necessary
docker-compose up -d
```

Comment out the following line in ```docker-compose.yml``` for production.

```yml
- --certificatesresolvers.letsencrypt.acme.caserver=https://acme-staging-v02.api.letsencrypt.org/directory
```
