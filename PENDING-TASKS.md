# Tarefas Pendentes

Priorizadas. Atualizar conforme avança.

> **Checkpoint 2026-10-08:** o DeskcommCRM está em produção e EM USO REAL no consultório (upgrade 1.27.1 → 1.76.0, canais waha + zernio ativos, IA gerando respostas, backups configurados). Várias tarefas abaixo datam de 2026-09-20 e precisam ser reavaliadas — as chaves "VAZIAS" no `.env` continuam vazias, mas o sistema funciona via `OPENROUTER_API_KEY`.

## ✅ CONCLUÍDO DESDE 2026-09-28

- [x] Upgrade do DeskcommCRM para **1.76.0** (containers recreados)
- [x] **Backup local diário** configurado (`0 3 * * *` → `backup.sh`, 14 retenções)
- [x] **Backup offsite B2** configurado (`40 3 * * *` → `/opt/backup-b2.sh`)
- [x] Sistema em **produção com uso real** — canais WhatsApp (waha) + zernio ativos, IA atendendo (30 chamadas LLM/24h)
- [x] **Traefik removido** — Caddy é o único proxy em 80/443

## 🔴 CRÍTICAS — bloqueiam valor completo do sistema

- [ ] **Rotacionar root password do VPS** (ainda não rotacionado desde a exposição em chat — 18 dias)
- [ ] Investigar `webhook_events_log_provider_check` — constraint violada 4x/24h, webhooks ficam sem log (canal `zernio` não está na constraint do banco)
- [ ] Investigar `[prospecting.cron] tickProspecting lançou` — erro 500 pontual (1x/24h, mas a rota responde 200 quando testada manualmente)
- [ ] Adquirir e configurar **ANTHROPIC_API_KEY** (ou decidir usar OpenRouter existente)
- [ ] Configurar **GOOGLE_CALENDAR_CLIENT_ID** e **GOOGLE_CALENDAR_CLIENT_SECRET**
- [ ] Verificar/instalar **AI_GATEWAY_API_KEY** (se usar OmniRoute como gateway)
- [ ] Testar integração Google Calendar após chaves configuradas

## 🟡 IMPORTANTES — melhoram a operação

- [ ] Adquirir **RESEND_API_KEY** + configurar domínio verificado
- [ ] Configurar **RESEND_FROM_EMAIL**
- [ ] Adquirir **OPENAI_API_KEY** (Whisper + RAG) — ⚠️ worker já chama `openai/gpt-4o` em 30 chamadas/24h; verificar de onde vem a credencial (pode ser via OmniRoute ou config da org, não do .env raiz)
- [ ] Gerar VAPID keys (`npx web-push generate-vapid-keys`) e configurar
- [ ] Preencher APP_LOGO_URL e APP_ACCENT_HEX para white-label (necessário para vender para outros consultórios)
- [ ] **Documentar o upgrade 1.27.1 → 1.76.0** (o que mudou, breaking changes) — importante para replicar em outros consultórios

## 🟢 POLIMIVO — melhoram a experiência

- [ ] Configurar **SENTRY_DSN** (opcional)
- [ ] Configurar **SUPPORT_EMAIL** (e-mail de suporte visível)
- [ ] Instalar **Kiro AI** no OmniRoute (opcional)
- [ ] Explorar **JEV/TypeSafe** como classificador barato para filtro de LLM

## 🔐 SEGURANÇA

- [ ] **ROTacionar root password** do VPS (exposta em conversas anteriores) — ver CRÍTICAS
- [ ] Verificar se o token do scheduler (`INTERNAL_CRON_SECRET`) não está no repositório (está redacted ✅, mas confirmar em todo o histórico git)
- [ ] Considerar restringir porta 20128 (OmniRoute) — está em `0.0.0.0`, acessível da internet
- [ ] Revisar chaves expostas no .env — asegurar que não estão em repositórios públicos

## 📋 DO SECOND BRAIN

- [x] Manter este repositório atualizado
- [x] Checkpoint semanal (cron) lê e atualiza PENDING-TASKS.md
- [x] Documentar cada decisão em DECISOES.md
- [x] Configurar cron job de manutenção do Second Brain (cron ativo)

## 🚀 VENDA DO SERVIÇO

- [x] **Validar o sistema com uso real do consultório** — em produção desde ~set/2026, canais ativos, 2 semanas+ de operação real ✅
- [ ] Documentar processo de instalação para replicação (install.sh / docs)
- [ ] Criar proposta de valores (instalação + configuração + manutenção mensal)
- [ ] Identificar primeiros clientes potenciais
- [ ] **White-label** (APP_LOGO_URL, APP_ACCENT_HEX, APP_NAME) antes de vender para outros consultórios
