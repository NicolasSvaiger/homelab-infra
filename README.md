# 🚀 LauLab - HomeLab Infrastructure

> Infraestrutura pessoal desenvolvida para estudos, experimentação e hospedagem de aplicações .NET utilizando Docker, AWS e ferramentas modernas de observabilidade.

---

# 📖 Sobre o Projeto

O **LauLab** é um HomeLab desenvolvido com foco em boas práticas de infraestrutura, monitoramento e desenvolvimento de aplicações.

O projeto possui uma arquitetura modular baseada em Docker, utilizando Proxy Reverso, HTTPS automático, monitoramento, centralização de logs e documentação completa.

O objetivo é simular um ambiente próximo ao encontrado em empresas, permitindo estudar infraestrutura, DevOps e desenvolvimento .NET em um único ambiente.

---

# 🎯 Objetivos

* Aprender Infraestrutura como Código
* Centralizar serviços em Docker
* Utilizar Proxy Reverso
* Automatizar HTTPS
* Monitorar disponibilidade
* Centralizar logs
* Hospedar aplicações .NET
* Criar um ambiente escalável

---

# 🏗️ Arquitetura

```text
                           Internet
                               │
                        Cloudflare DNS
                               │
                               ▼
                  Nginx Proxy Manager
                               │
        ┌──────────┬──────────┬──────────┬──────────┐
        │          │          │          │          │
   Portainer   WireGuard   Uptime     Dozzle      Seq
                           Kuma
                               │
                     Futuras APIs .NET
```

---

# ☁️ Infraestrutura

* AWS EC2
* Ubuntu Server 24.04 LTS
* Docker
* Docker Compose
* Cloudflare
* Let's Encrypt
* GitHub

---

# 📦 Serviços

## 🏗️ Infrastructure

| Serviço             | Domínio                 | Status |
| ------------------- | ----------------------- | ------ |
| Nginx Proxy Manager | npm.laulab.com.br       | ✅      |
| Portainer           | portainer.laulab.com.br | ✅      |
| WireGuard           | vpn.laulab.com.br       | ✅      |

---

## 📊 Monitoring

| Serviço     | Domínio            | Status |
| ----------- | ------------------ | ------ |
| Uptime Kuma | kuma.laulab.com.br | ✅      |
| Dozzle      | logs.laulab.com.br | ✅      |
| Seq         | seq.laulab.com.br  | ✅      |

---

# 📁 Estrutura

```text
homelab-infra/
│
├── docker/
│   ├── infrastructure/
│   │   ├── nginx-proxy-manager/
│   │   ├── portainer/
│   │   └── wireguard/
│   │
│   ├── monitoring/
│   │   ├── uptime-kuma/
│   │   ├── dozzle/
│   │   └── seq/
│   │
│   ├── applications/
│   ├── databases/
│   └── observability/
│
├── docs/
├── scripts/
└── README.md
```

---

# 🛠️ Tecnologias

## Infraestrutura

* AWS EC2
* Ubuntu
* Docker
* Docker Compose

## Proxy

* Nginx Proxy Manager
* Cloudflare
* Let's Encrypt

## Monitoramento

* Uptime Kuma
* Dozzle
* Seq

## Desenvolvimento

* Git
* GitHub

---

# 📚 Documentação

Cada serviço possui sua própria documentação.

## Infrastructure

* Nginx Proxy Manager
* Portainer
* WireGuard

## Monitoring

* Uptime Kuma
* Dozzle
* Seq

---

# 🗺️ Roadmap

## ✅ Sprint 1 - Infrastructure

* Docker
* Docker Compose
* Nginx Proxy Manager
* Portainer
* WireGuard
* Cloudflare
* HTTPS

---

## ✅ Sprint 2 - Observability

* Uptime Kuma
* Dozzle
* Seq

---

## 🟡 Sprint 3 - Applications

* ASP.NET Core API
* SQL Server
* Redis
* RabbitMQ

---

## ⚪ Sprint 4 - CI/CD

* Jenkins
* GitHub Actions
* Deploy Automatizado

---

## ⚪ Sprint 5 - Production

* Backup Automatizado
* Dashboards
* Alertas
* Hardening
* Observabilidade Avançada

---

# 🔒 Segurança

* HTTPS em todos os serviços
* Certificados Let's Encrypt
* Proxy Reverso
* Docker Network compartilhada
* Persistência de dados
* Containers isolados

---

# 📊 Status do Projeto

| Área           | Status |
| -------------- | ------ |
| Infrastructure | ✅      |
| Monitoring     | ✅      |
| Applications   | 🟡     |
| Databases      | ⏳      |
| CI/CD          | ⏳      |

---

# 👨‍💻 Autor

**Nicolas Svaiger**

Desenvolvedor .NET apaixonado por infraestrutura, automação e arquitetura de software.

---

# 📌 Licença

Projeto desenvolvido para fins de estudo e evolução profissional.

