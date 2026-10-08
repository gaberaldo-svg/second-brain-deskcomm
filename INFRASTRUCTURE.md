# Infrastructure — VPS e Docker

## VPS HostGator

- **OS:** AlmaLinux 9.8 (Olive Jaguar)
- **CPU/RAM:** 1 vCPU / 2GB RAM
- **IP:** 143.95.162.178
- **SSH:** porta 22022, acesso root via chave ed25519 `hermes-mobile`
- **Password:** INITIAL_PASSWORD — **PRECISA SER ROTACIONADO**

## Node.js

- Node v22.23.2
- npm 10.9.8

## PM2

- **omniroute:** online, pid 33002, uptime 3D, 16.2MB, root

## Docker — containers do DeskcommCRM (verificado 2026-10-08)

**Versão do DeskcommCRM: 1.76.0** (era 1.27.1 em 2026-09-20 — upgrade de 49 patch versions)

| Container | Status | Ports |
|---|---|---|
| deskcommcrm-caddy-1 | Up 15h | 80→80, 443→443, 443/udp, 2019 |
| deskcommcrm-scheduler-1 | Up 15h (healthy) | — |
| deskcommcrm-worker-1 | Up 15h (healthy) | 8787 |
| deskcommcrm-app-1 | Up 15h (healthy) | 3000 |
| deskcommcrm-waha-1 | Up 2d | 3000 |
| deskcommcrm-redis-1 | Up 7d (healthy) | 6379 |
| deskcommcrm-srh-1 | Up 7d | — |

⚠️ **Traefik e hermes-agent não aparecem mais** em `docker ps` — o Traefik (serviço Hostinger/Coolify) foi removido ou parado; o hermes-agent também não está rodando como container. Confirmar se era intencional.

## Backups (novo)

- `0 3 * * *` → `bash hostgator-setup-kit/backup.sh` — backup local diário em `/opt/DeskcommCRM/backups/`
  - Gera `db-YYYYmmdd-HHMMSS.sql.gz` (~6MB) e `waha-*.tgz` (~1.3MB), mantém 14 cópias (~83MB total)
- `40 3 * * *` → `/opt/backup-b2.sh` — cópia offsite para Backblaze B2

Último backup concluído com sucesso em 2026-10-08 03:02.

## Proxy reverso

- **Caddy** (Docker) — porta 80/443, TLS automático via Let's Encrypt
- **Traefik** (Docker) — **NÃO ESTÁ MAIS RODANDO** (ausente do `docker ps` em 2026-10-08)
- **Nginx:** inativo

## Rede Docker

- `br-ce54d46b3a74` — bridge network dos containers do DeskcommCRM

## Volume/Data

- OmniRoute data dir: `/root/.omniroute/` (5.8 MB database)
- OmniRoute install: `/usr/lib/node_modules/omniroute/`
- DeskcommCRM: `/opt/DeskcommCRM/`
- Caddy data: volume Docker

## Crontab (VPS)

```
0 3 * * *   cd /opt/DeskcommCRM && bash hostgator-setup-kit/backup.sh   # backup local diário
40 3 * * *  /opt/backup-b2.sh                                           # backup offsite B2
*/5 * * * * cd /opt/DeskcommCRM && bash hostgator-setup-kit/agent.sh     # agent de manutenção
* * * * *   curl -fsS -H @"/opt/DeskcommCRM/.env.cron-drain" "https://secretariaborges.duckdns.org/api/v1/cron/event-log-drain"
```

Além disso, o container **scheduler** roda ~15 crons internos (agent-dispatcher, followup-flow-worker, campaign-worker, routing-worker, webhook-replay, channel-health, contact-avatars, storage-redaction, snooze-watcher, handoff-devolucao, proposta-travada, recover-stuck-messages, prospecting) via `crond` contra `http://app:3000/api/v1/cron/*` com `Authorization: Bearer $INTERNAL_CRON_SECRET`.

## Uptime

- **OmniRoute:** online há 6D, pid 341295, 27.9MB, root, 0 restarts
- **DeskcommCRM:** containers up há 15h (app/worker/scheduler/caddy) — provavelmente restart após upgrade para 1.76.0
- VPS: up há 7d 9h, load 0.03
- Disco: 27G/49G (58%)
- Memória: 1.1Gi/1.7Gi usados, 588Mi disponível, swap 1.0Gi/2.0Gi usado
