# Example Traefik Service - traefik/whoami

Deploy an instance of [traefik/whoami](https://hub.docker.com/r/traefik/whoami).

The main Traefik stack must already be running, as this service joins its external
network. Set `DEFAULT_NETWORK` in `.env` to match that network's name (`global` by
default).

## Usage

```sh
docker compose up -d
```
