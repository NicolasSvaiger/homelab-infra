# WireGuard (wg-easy)

> Serviço responsável por fornecer acesso seguro à infraestrutura do HomeLab através de uma VPN WireGuard.

---

# 📖 Visão Geral

O **WireGuard** é a solução de VPN adotada no HomeLab para permitir acesso remoto seguro aos serviços internos hospedados na AWS.

Para facilitar a administração dos clientes e peers, foi utilizada a interface **wg-easy**, que fornece um painel web intuitivo para gerenciamento das configurações da VPN.

Todo o acesso administrativo ao HomeLab deve ocorrer preferencialmente através da VPN.

---

# 🎯 Objetivo

Os principais objetivos da VPN são:

* Acesso remoto seguro ao HomeLab.
* Evitar exposição de portas administrativas.
* Administração dos serviços via rede privada.
* Criação simplificada de novos clientes.
* Distribuição de configurações através de QR Code.

---

# 🏗 Arquitetura

```text
                      Notebook / Desktop
                               │
                        Cliente WireGuard
                               │
                     Túnel VPN (51820/UDP)
                               │
                               ▼
                     AWS EC2 (wg-easy)
                               │
               ┌───────────────┼────────────────┐
               │               │                │
               ▼               ▼                ▼
          Portainer        Docker Host      Serviços
```

---

# 🌐 Fluxo de Conexão

```text
Cliente
   │
   ▼
WireGuard Client
   │
   ▼
Internet
   │
   ▼
AWS EC2
Porta 51820/UDP
   │
   ▼
wg-easy
   │
   ▼
Rede Docker
```

---

# 🚀 Motivação da Escolha

Foram avaliadas outras soluções de VPN.

## OpenVPN

### Prós

* Muito utilizada.
* Grande comunidade.

### Contras

* Configuração mais complexa.
* Menor desempenho.

---

## Tailscale

### Prós

* Muito simples.
* Excelente experiência.

### Contras

* Dependência de terceiros.
* Menor controle da infraestrutura.

---

## WireGuard (Escolhido)

### Motivos

* Excelente desempenho.
* Baixo consumo de recursos.
* Configuração simples.
* Criptografia moderna.
* Fácil gerenciamento com wg-easy.
* Código enxuto.
* Ideal para HomeLabs.

---

# 📂 Estrutura

```text
/home/ubuntu/docker/wireguard

├── docker-compose.yml
├── README.md
└── data/
    ├── wg0.conf
    └── wg0.json
```

---

# 🐳 Docker Compose

Arquivo responsável pela criação do container.

```text
docker-compose.yml
```

---

# 🌐 Redes Docker

| Rede    | Finalidade                          |
| ------- | ----------------------------------- |
| default | Rede do Compose                     |
| proxy   | Comunicação com Nginx Proxy Manager |

---

# 💾 Volumes

| Caminho | Finalidade           |
| ------- | -------------------- |
| ./data  | Configurações da VPN |

A pasta `data` contém:

* Configuração da VPN.
* Clientes.
* Chaves.
* Peers.
* Configurações do wg-easy.

> **Importante:** esta pasta não deve ser versionada no GitHub.

---

# 🔌 Portas

| Porta     | Uso                   |
| --------- | --------------------- |
| 51820/UDP | Túnel VPN             |
| 51821/TCP | Painel Administrativo |

---

# 🌎 Acesso

Painel administrativo

```text
https://vpn.laulab.com.br
```

Temporário

```text
http://IP_DA_EC2:51821
```

---

# ⚙ Variáveis de Ambiente

| Variável      | Descrição             |
| ------------- | --------------------- |
| WG_HOST       | IP público ou domínio |
| PASSWORD_HASH | Senha do painel       |
| TZ            | Timezone              |
| LANG          | Idioma                |

---

# 👥 Clientes

Cada dispositivo recebe um Peer.

Exemplos:

* Notebook
* Desktop
* Celular
* Tablet

Cada cliente possui:

* Chave pública
* Chave privada
* IP interno
* QR Code

---

# ➕ Criando um Cliente

1. Abrir o painel wg-easy.
2. Criar novo Peer.
3. Informar nome.
4. Gerar configuração.
5. Baixar arquivo `.conf` ou utilizar o QR Code.

---

# 📱 Cliente Mobile

Instalar:

* Android → WireGuard
* iOS → WireGuard

Importar utilizando o QR Code.

---

# 💻 Cliente Windows

Instalar o cliente oficial:

https://www.wireguard.com/install/

Importar o arquivo `.conf`.

---

# ▶ Primeira Inicialização

```bash
cd /home/ubuntu/docker/wireguard

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

```bash
docker compose pull
docker compose up -d
docker image prune -a
```

---

# 📋 Validação

Verificar Compose

```bash
docker compose config
```

Verificar container

```bash
docker ps
```

Healthcheck

```bash
docker inspect wg-easy
```

---

# 📜 Logs

Tempo real

```bash
docker logs -f wg-easy
```

Últimas linhas

```bash
docker logs --tail 100 wg-easy
```

---

# 📈 Monitoramento

Uso de recursos

```bash
docker stats wg-easy
```

Inspecionar

```bash
docker inspect wg-easy
```

---

# 💾 Backup

Realizar backup da pasta:

```text
data/
```

Exemplo:

```bash
tar -czvf wireguard-backup.tar.gz data
```

---

# 🔄 Restore

Restaurar a pasta `data` e iniciar novamente:

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
docker restart wg-easy
```

---

## Verificar portas

```bash
docker ps
```

---

## Verificar Healthcheck

```bash
docker inspect wg-easy
```

---

## Verificar peers

Entrar no painel administrativo e confirmar se os clientes estão cadastrados corretamente.

---

# 🔒 Segurança

Boas práticas adotadas:

* WireGuard utiliza criptografia moderna.
* Administração preferencial via VPN.
* Painel protegido por senha.
* Restart automático.
* Rotação de logs.
* Versionamento apenas do Docker Compose.
* Configurações sensíveis não são armazenadas no GitHub.
* Porta 51820/UDP permanece aberta.
* Porta 51821/TCP será removida do Security Group após publicação via Nginx Proxy Manager.

---

# 📌 Boas Práticas

* Não compartilhar arquivos `.conf`.
* Não versionar a pasta `data`.
* Revogar clientes não utilizados.
* Utilizar nomes descritivos para os peers.
* Atualizar a imagem periodicamente.

---

# 🚀 Evolução

No futuro a VPN será utilizada para:

* Administração do HomeLab.
* Deploy de aplicações.
* Acesso ao Portainer.
* Acesso ao Grafana.
* Acesso ao PostgreSQL.
* Acesso ao Redis.
* Administração da infraestrutura.

---

# 📚 Links Oficiais

* https://www.wireguard.com/
* https://github.com/wg-easy/wg-easy

---

# 📅 Changelog

## 2026-06-27

* Migração para estrutura padronizada do HomeLab.
* Integração com a rede Docker `proxy`.
* Padronização do Docker Compose.
* Configuração de timezone.
* Configuração de rotação de logs.
* Documentação inicial criada.
