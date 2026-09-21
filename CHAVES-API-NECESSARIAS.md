# Chaves de API Necessárias

Lista das chaves que precisam ser adquiridas/configuradas para o DeskcommCRM funcionar plenamente.

> **Nunca commitar valores reais.** Este arquivo lista apenas o que é preciso, não os valores.

---

## 🔴 Críticas (sem elas o sistema não entrega valor completo)

### 1. ANTHROPIC_API_KEY
- **Para:** Chat da IA (Claude) — `AI_PROVIDER=anthropic`
- **Como conseguir:** https://console.anthropic.com/ → API Keys
- **Custo:** pago (uso por token)
- **Status:** 🔴 NÃO CONFIGURADO
- **Alternativa:** Se não quiser pagar, mudar `AI_PROVIDER` para `openrouter` e usar a chave existente (sk-or-...3fb4)

### 2. AI_GATEWAY_API_KEY
- **Para:** Gateway de IA unificado (OmniRoute como gateway)
- **Como conseguir:** Depende do gateway escolhido — se usar OmniRoute como gateway, pode usar OPENROUTER_API_KEY ou configurar providers diretamente
- **Status:** 🔴 NÃO CONFIGURADO

### 3. GOOGLE_CALENDAR_CLIENT_ID + CLIENT_SECRET
- **Para:** Integração de agenda com Google Calendar (agendamento de consultas)
- **Como conseguir:**
  1. Google Cloud Console: https://console.cloud.google.com/
  2. Criar projeto → APIs & Services → OAuth consent screen
  3. Credentials → OAuth 2.0 Client ID (Tipo: Web application)
  4. Redirecionamentos autorizados: `https://secretariaborges.duckdns.org/api/auth/callback/google` (ou similar — ver docs DeskcommCRM)
- **Scopes necessários:** `calendar.readonly`, `calendar.events` (ou similar)
- **Status:** 🔴 NÃO CONFIGURADO

---

## 🟡 Importantes (functionalidade útil, sistema funciona sem)

### 4. RESEND_API_KEY + RESEND_FROM_EMAIL
- **Para:** E-mails transacionais (convite de equipe, notificações, export LGPD)
- **Como conquistar:**
  1. Conta no Resend: https://resend.com/
  2. Verificar domínio (ou usar resend.dev para teste — e-mails podem ir para spam)
  3. Gerar API key
  4. `RESEND_FROM_EMAIL` deve ser de um domínio verificado
- **Sem isso:** convites mostram link na tela, e-mails não são enviados
- **Status:** 🟡 NÃO CONFIGURADO

### 5. OPENAI_API_KEY
- **Para:** Whisper (transcrição de áudios WhatsApp) + embeddings do RAG
- **Como conquistar:** https://platform.openai.com/api-keys
- **Sem isso:** IA responde sem base de conhecimento, pede áudio em texto
- **Status:** 🟡 NÃO CONFIGURADO

---

## 🟢 Opcionais (polimento)

### 6. VAPID_PUBLIC_KEY + VAPID_PRIVATE_KEY
- **Para:** Web Push — notificação na bandeja do sistema com a aba fechada
- **Como gerar:** `npx web-push generate-vapid-keys`
- **Sem isso:** notificações aparecem só com o site aberto
- **Status:** 🟢 NÃO CONFIGURADO

### 7. SENTRY_DSN
- **Para:** Telemetria de erros com performance/replay
- **Status:** 🟢 NÃO CONFIGURADO (hoje: apenas Sentry da comunidade com dados anonimizados)

### 8. APP_LOGO_URL + APP_ACCENT_HEX
- **Para:** White-label — personalização visual
- **Status:** 🟢 NÃO CONFIGURADOS

---

## Plano de aquisição sugerido

1. **Primeiro:** ANTHROPIC_API_KEY (ou decidir usar OpenRouter existente) — impacto imediato no chat da IA
2. **Segundo:** GOOGLE_CALENDAR_CLIENT_ID/SECRET — impacto imediato no agendamento
3. **Terceiro:** RESEND_API_KEY — e-mails transacionais
4. **Quarto:** OPENAI_API_KEY — áudio/voz e RAG
5. **Quinto:** VAPID — Web Push
