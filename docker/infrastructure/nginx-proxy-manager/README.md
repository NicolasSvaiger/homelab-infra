# Nginx Proxy Manager

> Reverse Proxy responsável pelo gerenciamento centralizado do tráfego HTTP/HTTPS do HomeLab.

---

# 📖 Visão Geral

O **Nginx Proxy Manager (NPM)** é o serviço responsável por publicar todos os serviços internos do HomeLab na Internet de forma segura, utilizando HTTPS, certificados Let's Encrypt e integração com o Cloudflare.

No HomeLab, o NPM atua como ponto único de entrada para todas as aplicações, eliminando a necessidade de expor portas administrativas diretamente na Internet.

---

# 🎯 Objetivo

O objetivo principal do Nginx Proxy Manager é:

* Centralizar o acesso aos serviços.
* Gerenciar certificados SSL automaticamente.
* Publicar aplicações utilizando subdomínios.
* Facilitar a administração através de interface web.
* Reduzir a superfície de ataque da infraestrutura.

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
                 (80 / 443 / 81 - Admin)
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
        ▼                      ▼                      ▼
   Portainer              WireGuard             Futuras APIs
 portainer.laulab     vpn.laulab.com.br      api.laulab.com.br
```

---

# 🚀 Motivação da Escolha

Diversas soluções poderiam ser utilizadas como Reverse Proxy.

## Traefik

### Prós

* Integração automática com Docker
* Muito utilizado em Kubernetes

### Contras

* Curva de aprendizado elevada
* Configuração baseada em labels

---

## Caddy

### Prós

* Configuração extremamente simples
* HTTPS automático

### Contras

* Menor quantidade de recursos administrativos

---

## Nginx Proxy Manager (Escolhido)

### Motivos

* Interface gráfica intuitiva
* Renovação automática de certificados
* Fácil integração com Cloudflare
* Ideal para HomeLabs
* Excelente documentação
* Fácil manutenção

---

# 📂 Estrutura

```text
/home/ubuntu/docker/nginx-proxy-manager

├── docker-compose.yml
├── README.md
├── data/
└── letsencrypt/
```

---

# 🐳 Docker Compose

Arquivo responsável pela criação do serviço.

```text
docker-compose.yml
```

---

# 🌐 Rede Docker

| Rede  | Finalidade                                       |
| ----- | ------------------------------------------------ |
| proxy | Comunicação com todos os serviços web do HomeLab |

---

# 💾 Volumes

| Volume        | Finalidade           |
| ------------- | -------------------- |
| ./data        | Configurações do NPM |
| ./letsencrypt | Certificados SSL     |

---

# 🔌 Portas

| Porta | Uso                   |
| ----- | --------------------- |
| 80    | HTTP                  |
| 81    | Painel Administrativo |
| 443   | HTTPS                 |

---

# 🌎 Subdomínios

Atualmente planejados:

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

# ⚙ Variáveis de Ambiente

| Variável | Valor             |
| -------- | ----------------- |
| TZ       | America/Sao_Paulo |

---

# ▶ Primeira Inicialização

```bash
cd /home/ubuntu/docker/nginx-proxy-manager

docker compose up -d
```

---

# ⏹ Parar

```bash
docker compose down
```

---

# 🔄 Reiniciar

```bash
docker compose restart
```

---

# ⬆ Atualizar

Baixar nova imagem

```bash
docker compose pull
```

Aplicar atualização

```bash
docker compose up -d
```

Remover imagens antigas

```bash
docker image prune -a
```

---

# 📋 Validação

Validar Compose

```bash
docker compose config
```

Verificar container

```bash
docker ps
```

Verificar redes

```bash
docker network ls
```

---

# 📜 Logs

Tempo real

```bash
docker logs -f nginx-proxy-manager
```

Últimas linhas

```bash
docker logs --tail 100 nginx-proxy-manager
```

---

# 📈 Monitoramento

Uso de recursos

```bash
docker stats nginx-proxy-manager
```

Inspecionar container

```bash
docker inspect nginx-proxy-manager
```

---

# 💾 Backup

Itens importantes:

* Pasta `data`
* Pasta `letsencrypt`

Backup manual

```bash
tar -czvf npm-backup.tar.gz data letsencrypt
```

A infraestrutura também é protegida pelos Snapshots EBS da AWS.

---

# 🔄 Restore

Extrair backup

```bash
tar -xzvf npm-backup.tar.gz
```

Subir serviço

```bash
docker compose up -d
```

---

# 🔒 Segurança

Práticas adotadas:

* HTTPS obrigatório
* Certificados Let's Encrypt
* Cloudflare como DNS
* Porta 81 utilizada apenas para administração
* Rede Docker dedicada (`proxy`)
* Restart automático (`unless-stopped`)
* Rotação de logs
* Timezone padronizado
* Versionamento da infraestrutura no GitHub

---

# 🛠 Troubleshooting

## Container parado

```bash
docker compose up -d
```

---

## Validar Compose

```bash
docker compose config
```

---

## Reiniciar serviço

```bash
docker restart nginx-proxy-manager
```

---

## Recriar container

```bash
docker compose down
docker compose up -d
```

---

## Verificar portas

```bash
docker ps
```

---

## Verificar rede

```bash
docker network inspect proxy
```

---

# 📌 Boas Práticas

* Nunca expor serviços diretamente sem passar pelo NPM.
* Utilizar HTTPS para todos os serviços.
* Renovar certificados automaticamente.
* Evitar acesso administrativo por IP público.
* Utilizar VPN para administração sempre que possível.
* Manter imagens Docker atualizadas.
* Versionar todas as alterações no GitHub.

---

# 📚 Links Oficiais

* https://nginxproxymanager.com/
* https://github.com/NginxProxyManager/nginx-proxy-manager

---

# 📅 Changelog

## 2026-06-27

* Migração para estrutura padronizada do HomeLab.
* Integração com rede Docker `proxy`.
* Padronização do Docker Compose.
* Configuração de timezone.
* Configuração de rotação de logs.
* Documentação inicial criada.
