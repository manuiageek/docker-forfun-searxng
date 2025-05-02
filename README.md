## Description

This `docker-compose.yml` file deploys a Docker container for **SearXNG**, a privacy-respecting metasearch engine.

The `searxng` service uses the official `searxng/searxng:latest` image. It maps port `8080` inside the container to port `8000` on the host machine. The configuration is customized using a read-only mounted `settings.yml` file, and persistent data is stored in a local `./data` volume.

Two environment variables are used:
- `SEARXNG_SECRET` to secure the instance,
- `BASE_URL` to configure the base URL accessible locally.

To generate a new SEARXNG_SECRET, you can use this command : 
openssl rand -hex 32

These variables should be defined in a `.env` file located in the same directory as the `docker-compose.yml` file.

The container is configured to always restart automatically using `restart: always`.

**Important:** Before starting the container, you need to create the external Docker network `searx_network` used by the service:

```bash
docker network create searx_network