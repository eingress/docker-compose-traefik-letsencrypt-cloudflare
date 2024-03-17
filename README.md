# Docker Compose Traefik + Lets Encrypt + Cloudflare

  A docker compose configuration script for spinning up a [Traefik](https://traefik.io/) instance with [Lets Encrypt DNS-01 challenge](https://letsencrypt.org/docs/challenge-types/#dns-01-challengw) supported through [Cloudflare](cloudflare.com).

## Usage

Generate the required compose, environment variable, and password files using ```generate-env``` (current Traefik versions may be edited at the top of this file)

```sh
./generate-env <output directory - defaults to current working directory>
```

Place compose.yml, .env, and .htpasswd in your chosen directory, then

```sh
docker compose pull
docker compose up -d
```

## Important

Comment out the following line in ```compose.yml``` for production.

```yml
- --certificatesresolvers.letsencrypt.acme.caserver=https://acme-staging-v02.api.letsencrypt.org/directory
```

See [examples](examples/) for how to configure services.
