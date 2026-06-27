# Seq

## Objetivo

O Seq é utilizado no LauLab como centralizador de logs estruturados, principalmente para aplicações .NET utilizando Serilog.

Ele permite visualizar, pesquisar e filtrar eventos de aplicação de forma organizada, facilitando debugging, troubleshooting e análise de comportamento dos sistemas.

---

# Arquitetura

```text
ASP.NET Core API
      │
      ▼
Serilog
      │
      ▼
Seq
      │
      ▼
Interface Web
```

---

# Estrutura de Diretórios

```text
seq/
├── data/
├── docker-compose.yml
└── README.md
```

---

# Docker Compose

Localização:

```text
docker/monitoring/seq/docker-compose.yml
```

---

# Persistência

Os dados ficam em:

```text
./data
```

Inclui:

* Eventos
* Usuários
* Configurações
* API Keys
* Dashboards
* Retenção

---

# Rede

Utiliza a rede Docker:

```text
proxy
```

---

# Proxy Reverso

Domínio:

```text
https://seq.laulab.com.br
```

Forward no Nginx Proxy Manager:

```text
seq:80
```

---

# Portas

| Porta | Uso                      |
| ----- | ------------------------ |
| 80    | Interface Web            |
| 5341  | Ingestão de logs Serilog |

---

# Variáveis de Ambiente

| Variável                   | Descrição             |
| -------------------------- | --------------------- |
| ACCEPT_EULA                | Aceite da licença     |
| SEQ_FIRSTRUN_ADMINUSERNAME | Usuário admin inicial |
| SEQ_FIRSTRUN_ADMINPASSWORD | Senha admin inicial   |
| TZ                         | Timezone              |

---

# Uso com .NET e Serilog

Exemplo de configuração futura:

```csharp
builder.Host.UseSerilog((context, configuration) =>
{
    configuration
        .ReadFrom.Configuration(context.Configuration)
        .WriteTo.Console()
        .WriteTo.Seq("http://seq:5341");
});
```

---

# Atualização

```bash
cd ~/homelab-infra/docker/monitoring/seq
sudo docker compose pull
sudo docker compose up -d
sudo docker image prune -f
```

---

# Logs

```bash
sudo docker logs seq --tail 100
sudo docker logs -f seq
```

---

# Troubleshooting

Validar compose:

```bash
sudo docker compose config
```

Verificar container:

```bash
sudo docker ps --filter name=seq
```

Reiniciar:

```bash
sudo docker restart seq
```

Verificar porta interna:

```bash
curl -I http://seq:80
```

---

# Backup

Backup da pasta:

```text
data/
```

Exemplo:

```bash
tar -czvf seq-backup.tar.gz data
```

---

# Restore

```bash
tar -xzvf seq-backup.tar.gz
sudo docker compose up -d
```

---

# Definition of Done

* Docker Compose criado
* Variáveis obrigatórias configuradas
* Container saudável
* HTTPS ativo
* Proxy Host configurado
* Monitor no Uptime Kuma
* README criado
* Versionado no Git

---

# Próximas Evoluções

* Criar API ASP.NET Core de exemplo
* Configurar Serilog
* Criar API Key
* Criar dashboards
* Criar alertas
* Definir política de retenção

---

# Versão

Sprint 2 - Observabilidade

Serviço implantado no projeto LauLab HomeLab.

