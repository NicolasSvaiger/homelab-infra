# HomeLab Infra

Infraestrutura pessoal em AWS usando Docker, WireGuard, Portainer e Nginx Proxy Manager.

## Serviços

- AWS EC2 Ubuntu
- Docker e Docker Compose
- WireGuard / wg-easy
- Portainer
- Nginx Proxy Manager
- AWS Systems Manager
- Snapshots automáticos
- Cloudflare DNS
- Let's Encrypt

## Estrutura

```text
docker/
├── infrastructure/
│   ├── wireguard/
│   ├── portainer/
│   └── nginx-proxy-manager/
├── applications/
├── databases/
└── observability/
