# Decisões — Log

Data | Decisão | Rationale | Status
---|---|---|---
2026-09-20 | Escolher OmniRoute como AI Gateway | Vídeo TypeSafe mostrou valor de classificação barata; OmniRoute já instalado e com providers | ✅ Implementado
2026-09-20 | AI_PROVIDER=anthropic | Preferência por Claude para qualidade no chat | 🔴 Chave falta
2026-09-20 | Usar OpenRouter como fallback | Chave sk-or-...3fb4 já disponível; garante IA funcionando mesmo sem Anthropic | ✅ Funcional
2026-09-20 | Caddy como reverse proxy (não Traefik/Nginx) | Caddy mais simples para TLS automático; Traefik já existia no VPS mas era de outro serviço | ✅ Implementado
2026-09-20 | Nginx mantido inativo | Conflito de ports com Caddy/Traefik | ✅ Decisão mantida
2026-09-20 | WAHA NOWEB engine | Modo sem interface web — mais leve, suficiente para integração via API | ✅ Implementado
2026-09-20 | WHATSAPP_RESTART_ALL_SESSIONS=True | Garante que sessões pareadas sobrevivem restart do container | ✅ Implementado
2026-09-20 | Voz (chamada WhatsApp) desligada | Risco de banimento da conta — não vale o risco para MVP | ✅ Decisão mantida
2026-09-20 | Weightlist JEV — esperar estabilidade antes de usar em produção | JEV ainda em weightlist, acesso via OpenRouter (instável) | 🟡 Monitorar
2026-09-20 | Second Brain no GitHub (público) | Centralizar contexto do projeto; facilitar checkpoint automático via cron | ✅ Criado
2026-09-20 | Cron de checkpoint a cada 2 dias | Avaliar andamento, sugerir próximos passos sem sobrecarga | 🔜 Criar
2026-09-20 | Cron de manutenção do Second Brain | Análise semanal da implementação e manutenção do repositório | 🔜 Criar

2026-09-21 | Verificação do OmniRoute: config dir existe e está funcional | `/root/.omniroute/` contém `.env` e `storage.sqlite`; PM2 online com pid 33002, uptime 3D, 39.1MB | ✅ Confirmado
2026-09-21 | Verificação dos containers DeskcommCRM | Todos os 8 containers up (3 dias), saúde ok, ports conforme esperado | ✅ Confirmado

## Próximas decisões a tomar

1. **Anthropic vs OpenRouter como provider principal** — decidir após adquirir ANTHROPIC_API_KEY
2. **Investir em JEV/TypeSafe?** — esperar estabilidade, validar caso de uso de classificação
3. **Schema de valores para venda do serviço** — instalação fixa + manutenção mensal

---

### 2026-09-28 | Cron de Checkpoint Semanal ativo | Implementado via cron job no Hermes Agent | ✅ Implementado
### 2026-09-28 | Cron de Manutenção do Second Brain ativo | Execução semanal de verificação do repositório | ✅ Implementado

---

## 2026-10-08 — Checkpoint Semanal

| Data | Decisão | Rationale | Status |
|---|---|---|---|
| 2026-10-08 | DeskcommCRM está **em produção com uso real** | 30 chamadas LLM/24h, canais waha+zernio ativos, flywheel rodando, sync de 467 modelos do OpenRouter. Não é mais um projeto de setup — é operação | ✅ Confirmado |
| 2026-10-08 | Upgrade **1.27.1 → 1.76.0** aconteceu fora do Second Brain | 49 patch versions de evolução sem documentação. Precisamos documentar antes de replicar para outros consultórios | ⚠️ Documentar |
| 2026-10-08 | **Traefik removido**, Caddy é o único proxy | Sem conflito de portas 80/443; serviço Hostinger/Coolify apparently descontinuado no VPS | ✅ Confirmado |
| 2026-10-08 | **Backups automatizados** (local + B2 offsite) | backup.sh diário com 14 retenções + backup-b2.sh. Último run OK em 2026-10-08 03:02 | ✅ Implementado |
| 2026-10-08 | `AI_PROVIDER=anthropic` sem `ANTHROPIC_API_KEY` | Worker real usa `openai/gpt-4o` (30x/24h) e `anthropic` (15x/24h) — as credenciais vêm da config da organização no Supabase, não do .env raiz. Documentação imprecisa | ⚠️ Corrigir docs |
| 2026-10-08 | Dois bugs recorrentes a investigar | `webhook_events_log_provider_check` (4x/24h) e `tickProspecting lançou` (1x/24h) | 🔴 Pendente |

## Próximas decisões a tomar

1. **Como a IA está autenticada?** — o `.env` mostra `ANTHROPIC_API_KEY=""` e `OPENAI_API_KEY=""` mas o worker chama ambos os providers. As chaves estão na config da organização (Supabase) ou no OmniRoute? Precisa ser documentado para replicação.
2. **Corrigir o bug da constraint `webhook_events_log_provider_check`** — o canal `zernio` não está na constraint do banco; é migração do schema ou bug da app?
3. **Rotacionar root password** — 18 dias desde a exposição. Prioridade máxima de segurança.
4. **Investir em JEV/TypeSafe?** — esperar estabilidade, validar caso de uso de classificação.
5. **Schema de valores para venda do serviço** — instalação fixa + manutenção mensal
