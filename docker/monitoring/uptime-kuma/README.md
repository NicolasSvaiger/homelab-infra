# Uptime Kuma

## Objetivo

O Uptime Kuma é a solução de monitoramento utilizada no HomeLab para verificar continuamente a disponibilidade dos serviços publicados.

Além do monitoramento HTTP, ele suporta monitoramento via TCP, Ping, DNS, Push e diversos outros protocolos.

No LauLab ele é responsável por monitorar toda a infraestrutura e futuramente também as aplicações, bancos de dados e APIs.

---

# Arquitetura

```
Internet
     │
     ▼
Cloudflare
     │
     ▼
Nginx Proxy Manager
     │
     ▼
Uptime Kuma
     │
     ├── LauLab
     ├── Nginx Proxy Manager
     ├── Portainer
     ├── WireGuard
     └── Futuras APIs
```

---

# Estrutura de Diretórios

```
uptime-kuma/
├── data/
├── docker-compose.yml
└── README.md
```

---

# Docker Compose

Localização:

```
docker/monitoring/uptime-kuma/docker-compose.yml
```

---

# Persistência

Todos os dados ficam armazenados em:

```
./data
```

Incluindo:

* Configurações
* Usuários
* Monitores
* Histórico
* Status Pages
* Tags

---

# Rede

O serviço utiliza a rede Docker compartilhada:

```
proxy
```

Isso permite comunicação com:

* Nginx Proxy Manager
* Portainer
* WireGuard
* Demais containers

---

# Proxy Reverso

Domínio:

```
https://kuma.laulab.com.br
```

Gerenciado pelo:

* Nginx Proxy Manager

SSL:

* Let's Encrypt

---

# Monitoramento Atual

## Infrastructure

* 🌐 LauLab
* ⚙️ Nginx Proxy Manager
* 📦 Portainer
* 🔐 WireGuard

---

# Grupos

Atualmente existem os grupos:

* 🏗️ Infrastructure
* 📊 Monitoring
* 💻 Applications
* 🗄️ Databases
* 🛠️ Development

---

# Tags

Exemplos de tags utilizadas:

* Infrastructure
* Website
* Proxy
* Container
* VPN

---

# Backup

O backup consiste apenas da pasta:

```
data/
```

Recomenda-se realizar backup antes de atualizações.

---

# Atualização

Entrar na pasta:

```bash
cd ~/homelab-infra/docker/monitoring/uptime-kuma
```

Baixar nova imagem:

```bash
sudo docker compose pull
```

Recriar container:

```bash
sudo docker compose up -d
```

Remover imagens antigas:

```bash
sudo docker image prune -f
```

---

# Logs

Visualizar logs:

```bash
sudo docker logs uptime-kuma
```

Últimas linhas:

```bash
sudo docker logs uptime-kuma --tail 100
```

Acompanhar em tempo real:

```bash
sudo docker logs -f uptime-kuma
```

---

# Troubleshooting

Verificar status:

```bash
sudo docker ps --filter name=uptime-kuma
```

Validar compose:

```bash
sudo docker compose config
```

Reiniciar:

```bash
sudo docker restart uptime-kuma
```

Parar:

```bash
sudo docker stop uptime-kuma
```

Iniciar:

```bash
sudo docker start uptime-kuma
```

---

# Comandos Úteis

Entrar na pasta:

```bash
cd ~/homelab-infra/docker/monitoring/uptime-kuma
```

Subir serviço:

```bash
sudo docker compose up -d
```

Parar serviço:

```bash
sudo docker compose down
```

Visualizar containers:

```bash
sudo docker ps
```

Inspecionar container:

```bash
sudo docker inspect uptime-kuma
```

---

# Definition of Done

Para considerar este serviço concluído, os seguintes itens devem estar atendidos:

* Docker Compose criado
* Persistência configurada
* HTTPS ativo
* Proxy Host configurado
* Rede Docker compartilhada
* Domínio publicado
* Certificado Let's Encrypt
* Documentação criada
* Serviço monitorando a infraestrutura

---

# Próximas Evoluções

* Configuração de notificações (Discord)
* Alertas por e-mail
* Monitoramento das APIs .NET
* Monitoramento de SQL Server
* Monitoramento do Redis
* Status Page pública
* Integração com Healthchecks
* Integração com GitHub Actions

---

# Versão

Sprint 2 - Observabilidade

Serviço implantado no projeto LauLab HomeLab.

