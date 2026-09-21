# Tarefas Pendentes

Priorizadas. Atualizar conforme avança.

## 🔴 CRÍTICAS — bloqueiam valor completo do sistema

- [ ] Adquirir e configurar **ANTHROPIC_API_KEY** (ou decidir usar OpenRouter existente)
- [ ] Configurar **GOOGLE_CALENDAR_CLIENT_ID** e **GOOGLE_CALENDAR_CLIENT_SECRET**
- [ ] Verificar/instalar **AI_GATEWAY_API_KEY** (se usar OmniRoute como gateway)
- [ ] Testar integração Google Calendar após chaves configuradas

## 🟡 IMPORTANTES — melhoram a operação

- [ ] Adquirir **RESEND_API_KEY** + configurar domínio verificado
- [ ] Configurar **RESEND_FROM_EMAIL**
- [ ] Adquirir **OPENAI_API_KEY** (Whisper + RAG)
- [ ] Gerar VAPID keys (`npx web-push generate-vapid-keys`) e configurar
- [ ] Preencher APP_LOGO_URL e APP_ACCENT_HEX para white-label

## 🟢 POLIMIVO — melhoram a experiência

- [ ] Configurar **SENTRY_DSN** (opcional)
- [ ] Configurar **SUPPORT_EMAIL** (e-mail de suporte visível)
- [ ] Instalar **Kiro AI** no OmniRoute (opcional)
- [ ] Explorar **JEV/TypeSafe** como classificador barato para filtro de LLM

## 🔐 SEGURANÇA

- [ ] **ROTacionar root password** do VPS (exposta em conversas anteriores)
- [ ] Revisar chaves expostas no .env — asegurar que não estão em repositórios públicos

## 📋 DO SECOND BRAIN

- [ ] Manter este repositório atualizado
- [ ] Checkpoint seminal (cron) lê e atualiza PENDING-TASKS.md
- [ ] Documentar cada decisão em DECISOES.md

## 🚀 VENDA DO SERVIÇO

- [ ] Validar o sistema com uso real do consultório (mínimo 2 semanas)
- [ ] Documentar processo de instalação para replicação (install.sh / docs)
- [ ] Criar proposta de valores (instalação + configuração + manutenção mensal)
- [ ] Identificar primeiros clientes potenciais
