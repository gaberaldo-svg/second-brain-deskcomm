# Cron Jobs — Configurados

## VPS (AlmaLinux, root)

### 1. Agent script (every 5min)
```
*/5 * * * * cd /opt/DeskcommCRM && bash hostgator-setup-kit/agent.sh >/dev/null 2>&1
```
- **Para:** Manutencao automatica do Kit HostGator (verifica/contém o ambiente)
- **Status:** ✅ Ativo

### 2. Event log drain (every 1min)
```
* * * * * curl -fsS -H "Authorization: Bearer ****" "https://secretariaborges.duckdns.org/api/v1/cron/event-log-drain" >/dev/null 2>&1
```
- **Para:** Drenar logs de eventos do DeskcommCRM (evita acumulo)
- **Status:** ✅ Ativo
- **Nota:** Bearer token real esta no crontab do VPS — nunca commitar

## Hermes (Windows, agente)

### 3. Checkpoint Semanal do Projeto (pending)
- **Schedule:** Cada 2 dias
- **Para:** Ler PENDING-TASKS.md, INFRASTRUCTURE.md, CONFIGURACAO-DESKCOMMCRM.md e sugerir proximos passos
- **Status:** 🔜 Criar via cronjob_manage

### 4. Manutencao do Second Brain (pending)
- **Schedule:** Semanal
- **Para:** Analisar se o repositorio esta atualizado, se documentos refletem estado real, sugerir melhorias na estrutura
- **Status:** 🔜 Criar via cronjob_manage
