# Containers Reverse Proxy

A reverse proxy for routing Docker containers using nginx and [docker-gen](https://github.com/jwilder/docker-gen).

## How to run

Build and run on Docker Compose.

```sh
docker-compose build
docker-compose up -d
```

Generated nginx configuration can be shown as follows:

```sh
docker-compose exec generator cat /etc/nginx/conf.d/map/generated
```

## How to connect containers and the reverse proxy

Add environment variable(s) and the network to containers as follows:

```yaml
version: "2"
services:
  app:
    image: node
    environment:
      # Virtual host name for the container.
      VIRTUAL_HOST: app.example.com
      # (Optional) Virtual host port. Defaults to exposed port or 80.
      VIRTUAL_PORT: 8080
    networks:
      - default
      - reverse-proxy-network

networks:
  reverse-proxy-network:
    external:
      # Docker network name.
      name: containersreverseproxy_default
```

## Contribution

This is an open source software licensed under Apache-2.0. Feel free to open issues or pull requests.
