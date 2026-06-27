# 🏠 HomeLab AWS

> Infraestrutura pessoal desenvolvida para estudos, desenvolvimento, automação e boas práticas de DevOps utilizando AWS, Docker e serviços Open Source.

---

# 📖 Sobre o Projeto

O **HomeLab AWS** é um ambiente hospedado na Amazon Web Services criado para simular uma infraestrutura próxima à utilizada em ambientes corporativos.

O projeto tem como objetivos:

* Aprender infraestrutura moderna.
* Hospedar aplicações .NET.
* Automatizar deploys.
* Centralizar gerenciamento dos containers.
* Monitorar serviços.
* Documentar toda a infraestrutura.
* Aplicar boas práticas de segurança.

Todo o ambiente é versionado no GitHub e documentado para facilitar futuras expansões.

---

# 🎯 Objetivos

* Centralizar toda a infraestrutura em Docker.
* Utilizar apenas serviços Open Source.
* Automatizar processos.
* Reduzir exposição de portas públicas.
* Utilizar HTTPS em todos os serviços.
* Versionar toda a infraestrutura.
* Facilitar recuperação da infraestrutura em caso de desastre.

---

# ☁️ Infraestrutura

```text
AWS
└── EC2 Ubuntu 24.04
    ├── Docker Engine
    ├── Docker Compose
    ├── Portainer
    ├── Nginx Proxy Manager
    ├── WireGuard (wg-easy)
    ├── Amazon SSM
    └── Cloudflare DNS
```

---

# 🏗 Arquitetura

```text
                               Internet
                                   │
                                   ▼
                            Cloudflare DNS
                                   │
                                   ▼
                            laulab.com.br
                                   │
                                   ▼
                      Nginx Proxy Manager
                                   │
        ┌──────────────────────────┼──────────────────────────┐
        │                          │                          │
        ▼                          ▼                          ▼
   Portainer                  WireGuard                 Futuras APIs
        │
        ▼
 Docker Engine
        │
        ▼
 Containers
```

---

# 📂 Estrutura do Projeto

```text
homelab-infra
│
├── README.md
│
├── docker
│   ├── infrastructure
│   │   ├── nginx-proxy-manager
│   │   ├── portainer
│   │   └── wireguard
│   │
│   ├── applications
│   ├── databases
│   └── observability
│
├── docs
│
└── scripts
```

---

# 🧩 Serviços

| Serviço             | Função               | Status |
| ------------------- | -------------------- | ------ |
| Nginx Proxy Manager | Reverse Proxy        | ✅      |
| Portainer           | Gerenciamento Docker | ✅      |
| WireGuard           | VPN                  | ✅      |
| Cloudflare          | DNS                  | ✅      |
| Amazon SSM          | Administração        | ✅      |

---

# 🌐 Domínios

| Domínio                 | Serviço      |
| ----------------------- | ------------ |
| laulab.com.br           | Landing Page |
| portainer.laulab.com.br | Portainer    |
| vpn.laulab.com.br       | WireGuard    |
| api.laulab.com.br       | APIs         |
| grafana.laulab.com.br   | Grafana      |
| kuma.laulab.com.br      | Uptime Kuma  |
| seq.laulab.com.br       | Seq          |

---

# 🔒 Segurança

A infraestrutura segue algumas práticas básicas de segurança:

* HTTPS em todos os serviços.
* Cloudflare como provedor DNS.
* Certificados Let's Encrypt.
* Administração via Amazon SSM.
* VPN WireGuard para acesso administrativo.
* Docker com restart automático.
* Rotação de logs.
* Volumes persistentes.
* Infraestrutura versionada no GitHub.

---

# 📚 Documentação

Cada serviço possui documentação própria.

| Serviço             | Documentação                                        |
| ------------------- | --------------------------------------------------- |
| Nginx Proxy Manager | docker/infrastructure/nginx-proxy-manager/README.md |
| Portainer           | docker/infrastructure/portainer/README.md           |
| WireGuard           | docker/infrastructure/wireguard/README.md           |

---

# 🚀 Roadmap

## Infraestrutura

* [x] AWS EC2
* [x] Docker
* [x] Docker Compose
* [x] Portainer
* [x] Nginx Proxy Manager
* [x] WireGuard
* [x] Amazon SSM
* [x] Cloudflare

## Observabilidade

* [ ] Uptime Kuma
* [ ] Dozzle
* [ ] Seq
* [ ] Grafana
* [ ] Prometheus

## Banco de Dados

* [ ] PostgreSQL
* [ ] Redis
* [ ] pgAdmin

## Desenvolvimento

* [ ] APIs .NET
* [ ] GitHub Actions
* [ ] CI/CD
* [ ] Deploy Automático

---

# 💾 Backup

A estratégia atual de backup é composta por:

* Snapshots EBS da AWS.
* Volumes Docker persistentes.
* Versionamento da infraestrutura no GitHub.

---

# 📈 Próximos Passos

As próximas etapas previstas para evolução do HomeLab são:

1. Finalizar configuração do domínio.
2. Publicar Portainer via HTTPS.
3. Publicar WireGuard via HTTPS.
4. Implantar observabilidade.
5. Configurar deploy automatizado.
6. Hospedar aplicações .NET.

---

# 👨‍💻 Autor

**Nicolas Svaiger**

Desenvolvedor .NET com foco em backend, infraestrutura, Docker e automação.

---

# 📅 Histórico

## 2026-06-27

* Criação da estrutura inicial do HomeLab.
* Migração dos serviços para estrutura padronizada.
* Documentação completa dos serviços.
* Versionamento da infraestrutura no GitHub.
