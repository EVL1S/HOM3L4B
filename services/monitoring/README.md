# Monitoring Stack

Prometheus + Grafana + Node Exporter for homelab observability.

## Deployment

- **Host:** node02 (192.168.10.3)
- **Stack:** Docker Compose (`~/docker/monitoring/`)
- **Grafana UI:** http://192.168.10.3:3001
- **Prometheus:** port 9090 (host network)

## Components

- **Prometheus** — metrics collection, `network_mode: host`
- **Grafana** — visualization, port 3001 (3000 occupied by AdGuard Home)
- **Node Exporter** — system metrics on node01 and node02, `network_mode: host`

## Networking notes

Grafana runs in Docker bridge network `monitoring_default` (172.19.0.x).
Prometheus datasource URL: `http://172.19.0.1:9090` (host IP from bridge network).
UFW allows Docker bridge range: `172.19.0.0/16` → port 9090.

## Node Exporter

Deployed on both nodes. Requires host filesystem mount for disk metrics:
```yaml
volumes:
  - /:/host:ro,rslave
command:
  - '--path.rootfs=/host'
```

## Dashboard

Node Exporter Full — Grafana dashboard ID `1860`.
