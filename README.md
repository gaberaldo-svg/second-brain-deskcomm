# Second Brain — DeskcommCRM

Repositório central de contexto do projeto: instalação, configuração, agentes de IA, integrações e manutenção do **DeskcommCRM** no consultório odontológico.

## Visão geral

- **Clínica:** Consultório Odontológico (secretariaborges.duckdns.org)
- **Sistema:** DeskcommCRM (self-hosted, Docker)
- **VPS:** HostGator — AlmaLinux 9.8, 1 vCPU / 2GB RAM, IP 143.95.162.178, SSH port 22022
- **Domínio:** secretariaborges.duckdns.org (DuckDNS)
- **Supabase:** jyjcqeubkncwuqehrbus.supabase.co
- **E-mail:** gabriel.borges.beraldo@gmail.com
- **Modelo de negócio:** Vender instalação + configuração + manutenção do DeskcommCRM para outros consultórios

## Repositório de infraestrutura

- **On-prem Docker:** `/opt/DeskcommCRM/` — docker-compose com Caddy, App, Worker, Scheduler, SRH, WAHA, Redis
- **AI Gateway:** OmniRoute v3.8.50 (PM2, porta 20128, online)
- **Proxy:** Caddy (Docker) nas portas 80/443

## Arquivos neste repositório

| Arquivo | Conteúdo |
|---|---|
| `INFRASTRUCTURE.md` | Detalhes do VPS, Docker, network, ports |
| `OMNIROUTE.md` | Configuração do AI Gateway OmniRoute, providers ativos |
| `CONFIGURACAO-DESKCOMMCRM.md` | Breakdown completo do .env, o que está preenchido e o que falta |
| `CHAVES-API-NECESSARIAS.md` | Lista das chaves de API que precisam ser adquiridas (sem valores reais) |
| `INTEGRACOES.md` | Google Calendar, WhatsApp/WAHA, Supabase, Resend, Web Push |
| `IA-AGENTS.md` | Agentes de IA planejados, contexto de uso, casos de uso |
| `PENDING-TASKS.md` | Tarefas pendentes ordenadas por prioridade |
| `DECISOES.md` | Log de decisões tomadas no projeto |
| `SEGUNDO-CECEBRO.md` | Este arquivo — propósito e como usar |
| `CRON-JOBS.md` | Cron jobs configurados (VPS + Hermes) |
| `VENDA-E-LANÇAMENTO.md` | Estratégia de venda do serviço de instalação/manutenção |

## Como usar

Este repositório é o "segundo cérebro" do projeto. Sempre que uma decisão é tomada, um arquivo é alterado ou um novo integração é configurada, atualiza-se o documento relevante aqui.

O agente de **Checkpoint Semanal** (cron) lê este repositório para avaliar o andamento e sugerir próximos passos.
