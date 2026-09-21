# Integrações

## Google Calendar

- **Estado:** 🔴 Não configurado
- **Variáveis:** `GOOGLE_CALENDAR_CLIENT_ID`, `GOOGLE_CALENDAR_CLIENT_SECRET` (ambos vazios)
- **Valor:** Agendamento de consultas odontológicas via calendário Google sincronizado com o DeskcommCRM
- **Ação necessária:** Ver `CHAVES-API-NECESSARIAS.md` (#3)

## WhatsApp (WAHA)

- **Estado:** ✅ Configurado e rodando
- **Engine:** `devlikeapro/waha:latest-2026.7.2-2026.7.2` (NOWEB)
- **API:** `http://waha:3000` (interno Docker)
- **Webhook:** `http://app:3000`
- **API Key:** configurada
- **HMAC Secret:** configurado
- **Restart sessions:** habilitado (`WHATSAPP_RESTART_ALL_SESSIONS=True`)
- **Webhook signature:** desligado (`WAHA_WEBHOOK_REQUIRE_SIGNATURE=false`)
- **Voz (chamada):** desligado — ligar vincula segundo aparelho, risco de banimento

## Supabase

- **Projeto:** `jyjcqeubkncwuqehrbus.supabase.co`
- **Anon key:** configurado (Frontend)
- **Service role key:** configurado (Backend)
- **DB URL:** postgresql://postgres.jyjcqeubkncwuqehrbus:***@aws-0-us-east-2.pooler.supabase.com:5432/postgres
- **Uso:** Banco de dados do DeskcommCRM (auth, dados, storage)

## Redis / Upstash

- **SRH (Serverless Redis HTTP):** `http://srh:80` (container Docker)
- **Token:** configurado
- **Uso:** Cache/queue do DeskcommCRM

## Resend (e-mails)

- **Estado:** 🔴 Não configurado
- **Status:** e-mails transacionais desligados

## Web Push (VAPID)

- **Estado:** 🟢 Não configurado
- **Status:** notificações apenas com site aberto

## Sentry

- **Estado:** 🟢 Não configurado (modo off)
- **Status:** apenas telemetria anonimizada da comunidade

## Traefik (existente, não-DeskcommCRM)

- **Container:** traefik (Up 31h)
- **Ports:** 18080→80, 18443→443
- **Origem:** Hostinger/Coolify/Dokploy (serviço pré-existente no VPS)
- **Impacto:** DeskcommCRM usa Caddy nas mesmas ports — cuidado com conflito

## Caddy (DeskcommCRM)

- **Container:** deskcommcrm-caddy-1
- **Ports:** 80→80, 443→443, 443/udp, 2019
- **TLS:** automático via Let's Encrypt (ACME_EMAIL configurado)
