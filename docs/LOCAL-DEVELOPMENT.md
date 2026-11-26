# Local development

This Compose stack is for local development only. It exposes WordPress on loopback, not the LAN, and uses disposable development passwords unless overridden. Do not use it as a production deployment.

## Start

From the repository root:

```sh
docker compose up -d
docker compose ps
docker compose logs --tail=100 wordpress db
```

Podman users can use `podman compose` or the installed `docker-compose` provider. Fully qualified Docker Hub image names avoid short-name prompts. The first launch may take a little time for MariaDB initialization.

Open http://localhost:8080 and complete WordPress setup. Install and activate **WooCommerce** from Plugins > Add New, then activate **Buy Control for WooCommerce** from the installed plugins list. Configure WooCommerce shipping and the RouteMile settings (some labels remain unchanged) and use OpenStreetMap for initial development.

The plugin source is mounted read-only in WordPress; edit the files from your host checkout. WordPress core, uploads, installed plugins and database persist in named volumes.

## Troubleshooting

- Port conflict: `WP_PORT=8081 docker compose up -d`.
- If database setup initially fails, wait until MariaDB is ready, then reload the installer.
- If Podman reports permission errors on a bind mount, check that the checkout is readable by the rootless container user. On NTFS or other non-Linux filesystems, try moving the checkout into your Linux home directory (ext4). On SELinux hosts, use an appropriate relabeled mount on a supported filesystem.
- PWA and geolocation generally require a secure context; localhost is suitable for many browser tests, but a phone on the LAN needs a separately configured HTTPS environment.
- Do not activate the original RouteMile plugin alongside Buy Control.

Stop with `docker compose down`. Named volumes remain. Do not add `-v` unless you intend to delete the local database and WordPress data.

Run the static suite on your host with `php tests/RouteWTestRunner.php`. The stack has not yet been runtime-validated on the maintainer's machine.
