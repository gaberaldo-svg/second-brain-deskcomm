# Configuracao — DeskcommCRM (.env)

Extraido do `/opt/DeskcommCRM/.env` (2026-09-20).

> **Aviso:** Este arquivo contem apenas metadados e status das chaves. Valores reais dos secrets ficam apenas no .env do VPS, nunca aqui.

## Preenchidos ✅

| Variavel | Valor | Observacao |
|---|---|---|
| DOMAIN | secretariaborges.duckdns.org | |
| ACME_EMAIL | gabriel.borges.beraldo@gmail.com | |
| REVERSE_PROXY | caddy | |
| NEXT_PUBLIC_SUPABASE_URL | https://jyjcqeubkncwuqehrbus.supabase.co | Publico — OK |
| NEXT_PUBLIC_SUPABASE_ANON_KEY | sb_publishable_**** (ver .env real) | Publico — OK |
| SUPABASE_SERVICE_ROLE_KEY | sb_secret_**** (ver .env real no VPS) | **SECRETO** |
| SUPABASE_DB_URL | postgresql://postgres.jyjcqeubkncwuqehrbus:***@****.supabase.com:5432/postgres | **SECRETO** |
| NEXT_PUBLIC_APP_URL | https://secretariaborges.duckdns.org | |
| NEXT_PUBLIC_ADMIN_URL | https://secretariaborges.duckdns.org | |
| APP_NAME | DeskcommCRM | |
| APP_LOCALE | pt-BR | |
| AI_PROVIDER | anthropic | |
| OPENROUTER_API_KEY | sk-or-**** (ver .env real no VPS) | **SECRETO** |
| NODE_ENV | production | |
| WAHA_API_BASE_URL | http://waha:3000 | Interno Docker |
| WAHA_WEBHOOK_BASE_URL | http://app:3000 | Interno Docker |
| WAHA_API_KEY | **** (ver .env real no VPS) | **SECRETO** |
| UPSTASH_REDIS_REST_URL | http://srh:80 | Interno Docker |
| UPSTASH_REDIS_REST_TOKEN | **** (ver .env real no VPS) | **SECRETO** |
| APP_IMAGE | ghcr.io/melgarafael/deskcommcrm:1.27.1 | |
| WORKER_IMAGE | ghcr.io/melgarafael/deskcomm-worker:1.27.1 | |
| SCHEDULER_IMAGE | ghcr.io/melgarafael/deskcomm-scheduler:1.27.1 | |
| INTERNAL_SECRET | **** (ver .env real no VPS) | **SECRETO** |
| INTERNAL_CRON_SECRET | **** (ver .env real no VPS) | **SECRETO** |
| WHATSAPP_RESTART_ALL_SESSIONS | True | |

## VAZIOS — precisam ser preenchidos 🔴

| Variavel | Para que serve | Prioridade |
|---|---|---|
| **ANTHROPIC_API_KEY** | Chat da IA (Claude) — e o AI_PROVIDER padrao | 🔴 Alta |
| **AI_GATEWAY_API_KEY** | Gateway de IA alternativo (OmniRoute) | 🔴 Alta |
| **GOOGLE_CALENDAR_CLIENT_ID** | Integracao calendario Google | 🔴 Alta |
| **GOOGLE_CALENDAR_CLIENT_SECRET** | Integracao calendario Google | 🔴 Alta |
| **RESEND_API_KEY** | E-mails transacionais (convite, etc.) | 🟡 Media |
| **RESEND_FROM_EMAIL** | E-mail transacional verificado no Resend | 🟡 Media |
| **OPENAI_API_KEY** | Whisper (transcricao audio WhatsApp) + embeddings RAG | 🟡 Media |
| **VAPID_PUBLIC_KEY** | Web Push notifications | 🟢 Baixa |
| **VAPID_PRIVATE_KEY** | Web Push notifications | 🟢 Baixa |
| **SENTRY_DSN** | Telemetria de erros (opcional) | 🟢 Baixa |
| **APP_LOGO_URL** | White-label — logo na sidebar | 🟢 Baixa |
| **APP_ACCENT_HEX** | Semente de cor (banco sobrescreve depois) | 🟢 Baixa |
| **SUPPORT_EMAIL** | E-mail de suporte visivel ao cliente final | 🟢 Baixa |

## Observacoes

- **AI_PROVIDER=anthropic** mas **ANTHROPIC_API_KEY** esta vazio → a IA pode estar caindo em fallback (OPENROUTER_API_KEY preenchido)
- **OPENROUTER_API_KEY** esta preenchido — prova de conceito funcional
- **Resend** sem chave = e-mails transacionais desligados (convite mostra link na tela)
- **Google Calendar** sem client ID/secret = integracao de agenda desligada
- **VAPID** vazios = Web Push apenas com site aberto (sem notificacao na bandeja)

## AÇÃO: Preencher as chaves 🔴

Ver `CHAVES-API-NECESSARIAS.md` para o plano de aquisicao das chaves.

## Regras de seguranca para este arquivo

- **Nunca** commitar valores reais de: INTERNAL_SECRET, INTERNAL_CRON_SECRET, WAHA_API_KEY, SUPABASE_SERVICE_ROLE_KEY, SUPABASE_DB_URL (senha), UPSTASH_REDIS_REST_TOKEN, OPENROUTER_API_KEY, AI_GATEWAY_API_KEY, ANTHROPIC_API_KEY, GOOGLE_CALENDAR_CLIENT_SECRET
- O anon key do Supabase e PUBLICO por design — pode ficar
- A URL do Supabase e PUBLICO — pode ficar
- Demais chaves: apenas status (preenchido/vazio) + referencia ao .env real do VPS
