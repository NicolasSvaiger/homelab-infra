# Dozzle

## Objetivo

O Dozzle é a ferramenta de visualização de logs em tempo real utilizada no LauLab.

Seu principal objetivo é facilitar a análise e troubleshooting dos containers Docker sem necessidade de acessar o terminal via SSH para consultar logs.

---

# Arquitetura

```
Usuário
    │
    ▼
Cloudflare
    │
    ▼
Nginx Proxy Manager
    │
    ▼
Dozzle
    │
    ▼
Docker Socket
    │
    ▼
Containers
```

---

# Estrutura de Diretórios

```
dozzle/
├── docker-compose.yml
└── README.md
```

---

# Docker Compose

Localização:

```
docker/monitoring/dozzle/docker-compose.yml
```

---

# Funcionamento

O Dozzle realiza leitura do Docker através do socket:

```
/var/run/docker.sock
```

A montagem é realizada em modo somente leitura (read-only):

```
/var/run/docker.sock:/var/run/docker.sock:ro
```

Isso permite visualizar logs sem alterar containers.

---

# Rede

O serviço utiliza a rede Docker compartilhada:

```
proxy
```

---

# Proxy Reverso

Domínio:

```
https://logs.laulab.com.br
```

Gerenciado por:

* Nginx Proxy Manager

SSL:

* Let's Encrypt

---

# Funcionalidades

* Logs em tempo real
* Busca por containers
* Pesquisa em logs
* Auto Refresh
* Interface Web
* Compatível com Docker

---

# Casos de Uso

* Verificar erros de inicialização
* Acompanhar logs em tempo real
* Troubleshooting de aplicações
* Monitorar reinicializações
* Identificar exceções rapidamente

---

# Segurança

O acesso é realizado através de HTTPS.

O socket Docker é montado em modo somente leitura para reduzir riscos.

---

# Atualização

Entrar na pasta:

```bash
cd ~/homelab-infra/docker/monitoring/dozzle
```

Atualizar imagem:

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
sudo docker logs dozzle
```

Últimas linhas:

```bash
sudo docker logs dozzle --tail 100
```

Tempo real:

```bash
sudo docker logs -f dozzle
```

---

# Troubleshooting

Validar compose:

```bash
sudo docker compose config
```

Verificar container:

```bash
sudo docker ps --filter name=dozzle
```

Reiniciar:

```bash
sudo docker restart dozzle
```

Parar:

```bash
sudo docker stop dozzle
```

Iniciar:

```bash
sudo docker start dozzle
```

---

# Comandos Úteis

Entrar na pasta:

```bash
cd ~/homelab-infra/docker/monitoring/dozzle
```

Subir:

```bash
sudo docker compose up -d
```

Parar:

```bash
sudo docker compose down
```

Inspecionar:

```bash
sudo docker inspect dozzle
```

---

# Definition of Done

Para considerar este serviço concluído:

* Docker Compose criado
* HTTPS configurado
* Proxy Host criado
* DNS configurado
* Rede proxy
* README criado
* Monitor configurado no Uptime Kuma
* Tags configuradas
* Grupo configurado

---

# Próximas Evoluções

* Autenticação adicional via Nginx Proxy Manager
* Integração com autenticação centralizada
* Filtros personalizados
* Exportação de logs
* Integração com Seq

---

# Versão

Sprint 2 - Observabilidade

Serviço implantado no projeto LauLab HomeLab.
