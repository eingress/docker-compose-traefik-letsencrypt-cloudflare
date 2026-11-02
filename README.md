# Docker Compose Traefik + Let's Encrypt + Cloudflare

A docker compose configuration generator script for [Traefik](https://traefik.io/) with the [Let's Encrypt DNS-01 challenge](https://letsencrypt.org/docs/challenge-types/#dns-01-challenge) supported through [Cloudflare](https://www.cloudflare.com/).

## Prerequisites

- Docker Compose and ```openssl```
- A DNS record pointing the Traefik dashboard host name at your server
- A [Cloudflare API token](https://dash.cloudflare.com/profile/api-tokens) with ```Zone:Read``` and ```DNS:Edit``` permissions for the zone

## Usage

Generate the required compose, environment variable, and password files using ```acdct``` (current Traefik versions may be edited at the top of this file)

```sh
./acdct [-f|--force] <output directory - defaults to current working directory>
```

Existing files are left untouched unless ```--force``` is given. Then, from the output directory

```sh
docker compose pull
docker compose up -d
```

## Important

Certificates come from the Let's Encrypt staging environment by default. Comment out the following line in ```compose.yaml``` for production.

```yml
- --certificatesresolvers.letsencrypt.acme.caserver=https://acme-staging-v02.api.letsencrypt.org/directory
```

Staging certificates already stored in the ```acme``` volume are not replaced when this line changes, so remove the volume at the same time. This also removes the stack's containers.

```sh
docker compose down --volumes
docker compose up -d
```

All HTTP traffic is redirected to HTTPS at the entrypoint, and the Traefik dashboard is published on the generated host name behind HTTP basic auth (credentials in ```.htpasswd```).

Services deployed alongside the stack join its external ```global``` network, and Traefik only routes to those labelled ```traefik.enable=true``` — see [examples](examples/) for how to configure services, and an example of generated output.

Traefik has access to the Docker socket, and read-only mounting does not limit what the Docker API allows. See [Traefik's guidance](https://doc.traefik.io/traefik/reference/install-configuration/providers/docker/) if you need to restrict it further.
