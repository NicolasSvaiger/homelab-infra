# Portainer

> Plataforma de gerenciamento de containers Docker utilizada como painel central de administração do HomeLab.

---

# 📖 Visão Geral

O **Portainer** é a interface gráfica responsável pelo gerenciamento da infraestrutura Docker do HomeLab.

Ele centraliza a administração dos containers, stacks, volumes, redes, imagens e ambientes Docker, permitindo uma gestão simplificada da infraestrutura sem depender exclusivamente do terminal.

No HomeLab, o Portainer é considerado o painel principal de administração da plataforma.

---

# 🎯 Objetivo

O Portainer tem como principais objetivos:

* Centralizar a administração dos containers Docker.
* Gerenciar Stacks utilizando Docker Compose.
* Administrar imagens, volumes e redes.
* Facilitar atualizações da infraestrutura.
* Permitir visualização de logs e estatísticas.
* Reduzir erros operacionais durante deploys.

---

# 🏗 Arquitetura

```text
                        Internet
                            │
                            ▼
                     Cloudflare DNS
                            │
                            ▼
                  Nginx Proxy Manager
                            │
                            ▼
              portainer.laulab.com.br
                            │
                            ▼
                     Portainer CE
                            │
        ┌───────────────────┼────────────────────┐
        │                   │                    │
        ▼                   ▼                    ▼
     Containers          Networks           Volumes
        │
        ├── WireGuard
        ├── Nginx Proxy Manager
        ├── APIs
        ├── Grafana
        ├── PostgreSQL
        └── Demais Serviços
```

---

# 🚀 Motivação da Escolha

Embora seja possível administrar Docker exclusivamente pelo terminal, o Portainer reduz significativamente o tempo de administração da infraestrutura.

Benefícios:

* Interface intuitiva.
* Deploy de Docker Compose (Stacks).
* Gerenciamento simplificado de containers.
* Atualizações com poucos cliques.
* Visualização centralizada de logs.
* Gerenciamento de redes Docker.
* Gerenciamento de volumes.
* Estatísticas de utilização.

---

# 📂 Estrutura

```text
/home/ubuntu/docker/portainer

├── docker-compose.yml
└── README.md
```

---

# 🐳 Docker Compose

Arquivo responsável pela criação do serviço.

```text
docker-compose.yml
```

---

# 🌐 Redes Docker

| Rede    | Finalidade                            |
| ------- | ------------------------------------- |
| default | Rede padrão do Compose                |
| proxy   | Comunicação com o Nginx Proxy Manager |

---

# 💾 Volumes

| Volume         | Finalidade                          |
| -------------- | ----------------------------------- |
| portainer_data | Persistência dos dados do Portainer |

Esse volume armazena:

* Usuários
* Senhas
* Endpoints
* Templates
* Configurações
* Stacks
* Tokens

---

# 🔌 Portas

| Porta | Uso          |
| ----- | ------------ |
| 9443  | HTTPS        |
| 9000  | HTTP interno |
| 8000  | Edge Agent   |

---

# 🌎 Acesso

Produção

```text
https://portainer.laulab.com.br
```

Temporário

```text
https://IP_DA_EC2:9443
```

---

# ⚙ Variáveis de Ambiente

| Variável | Valor             |
| -------- | ----------------- |
| TZ       | America/Sao_Paulo |

---

# ▶ Primeira Inicialização

```bash
cd /home/ubuntu/docker/portainer

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

# ⬆ Atualização

Atualizar imagem

```bash
docker compose pull
```

Aplicar atualização

```bash
docker compose up -d
```

Limpar imagens antigas

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

Verificar volume

```bash
docker volume ls
```

---

# 📜 Logs

Tempo real

```bash
docker logs -f portainer
```

Últimas linhas

```bash
docker logs --tail 100 portainer
```

---

# 📈 Monitoramento

Uso de recursos

```bash
docker stats portainer
```

Inspecionar

```bash
docker inspect portainer
```

---

# 💾 Backup

O Portainer utiliza o volume Docker:

```text
portainer_data
```

Consultar localização

```bash
docker volume inspect portainer_data
```

O backup é protegido pelos Snapshots EBS da AWS.

---

# 🔄 Restore

Após restaurar o volume:

```bash
docker compose up -d
```

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

## Reiniciar

```bash
docker restart portainer
```

---

## Recriar

```bash
docker compose down
docker compose up -d
```

---

## Entrar no container

```bash
docker exec -it portainer sh
```

---

## Verificar redes

```bash
docker network ls
```

---

## Verificar volumes

```bash
docker volume ls
```

---

# 🔒 Segurança

Boas práticas adotadas:

* HTTPS obrigatório.
* Acesso preferencial via Nginx Proxy Manager.
* Porta 9443 será removida do Security Group após configuração do domínio.
* Dados persistidos em volume Docker.
* Logs com rotação.
* Restart automático.
* Infraestrutura versionada no GitHub.
* Administração preferencial via VPN.

---

# 📌 Boas Práticas

* Gerenciar todos os serviços utilizando Stacks.
* Evitar alterações manuais diretamente nos containers.
* Versionar todos os Docker Compose.
* Atualizar imagens periodicamente.
* Utilizar o Portainer apenas para administração, mantendo os arquivos de infraestrutura no GitHub.

---

# 🚀 Evolução do HomeLab

O Portainer será responsável por administrar:

* Nginx Proxy Manager
* WireGuard
* PostgreSQL
* Redis
* Grafana
* Prometheus
* Uptime Kuma
* Seq
* APIs .NET
* Demais aplicações do HomeLab

---

# 📚 Links Oficiais

* https://www.portainer.io/
* https://docs.portainer.io/

---

# 📅 Changelog

## 2026-06-27

* Migração para estrutura padronizada.
* Integração com a rede `proxy`.
* Padronização do Docker Compose.
* Configuração de timezone.
* Configuração de rotação de logs.
* Documentação inicial criada.
