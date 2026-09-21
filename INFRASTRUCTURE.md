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

## Docker — containers do DeskcommCRM

| Container | Status | Ports |
|---|---|---|
| traefik | Up 31h | 18080→80, 18443→443 |
| deskcommcrm-caddy-1 | Up 3d | 80→80, 443→443, 443/udp, 2019 |
| deskcommcrm-scheduler-1 | Up 3d (healthy) | — |
| deskcommcrm-worker-1 | Up 3d (healthy) | 8787 |
| deskcommcrm-app-1 | Up 3d (healthy) | 3000 |
| deskcommcrm-srh-1 | Up 3d | — |
| deskcommcrm-waha-1 | Up 3d | 3000 |
| deskcommcrm-redis-1 | Up 3d (healthy) | 6379 |
| hermes-agent | Up 11m | — |

## Proxy reverso

- **Caddy** (Docker) — porta 80/443, TLS automático via Let's Encrypt
- **Traefik** (Docker, existente) — porta 18080→80, 18443→443 (serviço Hostinger/Coolify)
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
*/5 * * * * cd /opt/DeskcommCRM && bash hostgator-setup-kit/agent.sh >/dev/null 2>&1
* * * * * curl -fsS -H "Authorization: Bearer 5b855a...914c" "https://secretariaborges.duckdns.org/api/v1/cron/event-log-drain" >/dev/null 2>&1
```

## Uptime

- OmniRoute online há ~19h (segundo memória anterior)
- DeskcommCRM containers up há 3 dias
