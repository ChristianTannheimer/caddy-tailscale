# Caddy + Tailscale Docker Image

This repository provides an automated, up-to-date Docker image of [Caddy](https://caddyserver.com/) bundled with the [Tailscale plugin](https://github.com/tailscale/caddy-tailscale). 

## 🚀 Features
* **Always up-to-date:** A smart GitHub Action checks daily for new Caddy releases and Tailscale plugin updates.
* **Zero Downtime Updates:** It only builds and pushes a new image to the GitHub Container Registry (GHCR) if there is an actual change. No unnecessary rebuilds.
* **Watchtower-ready:** Perfect for automated server deployments using Watchtower.

## 📦 Usage

You can use this pre-built image directly in your `docker-compose.yml`. Don't forget to mount your Tailscale socket and a `/config` volume so Caddy keeps its authentication state!

```yaml
services:
  caddy:
    image: ghcr.io/christiantannheimer/caddy-tailscale:latest
    container_name: caddy
    restart: always
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
      - caddy_data:/data
      - caddy_config:/config
      - /var/run/tailscale/tailscaled.sock:/var/run/tailscale/tailscaled.sock

volumes:
  caddy_data:
  caddy_config:
