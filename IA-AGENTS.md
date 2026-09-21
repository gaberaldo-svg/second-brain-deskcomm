# Agentes de IA — Planejamento

## Contexto

O DeskcommCRM já tem IA integrada (chat, assistente). O OmniRoute atua como AI Gateway com múltiplos providers. O objetivo é:

1. **Uso interno do consultório:** agentes que ajudam a equipe do consultório a operar com mais eficiência
2. **Venda futura:** oferecer agentes personalizados como parte do pacote de manutenção

## Agentes planejados (uso pessoal → produto)

### 1. Agente de Agendamento (Scheduler Agent)
- **Função:** Verificar agenda do Google Calendar, sugerir horários disponíveis, confirmar consultas
- **IA:** LLM (Claude/OpenRouter) para entendimento de linguagem natural
- **Integração:** Google Calendar API + WhatsApp (WAHA)
- **Status:** 🔴 Pendente — depende de Google Calendar configurado

### 2. Agente de Follow-up de Pacientes
- **Função:** Identificar pacientes com consultas pendentes, enviar lembretes via WhatsApp
- **IA:** Classificação (JEV-inspired — ver vídeo TypeSafe) para identificar quem precisa de follow-up
- **Integração:** Supabase (dados de pacientes) + WAHA
- **Status:** 🟡 Em planejamento

### 3. Agente de Respostas para WhatsApp (Sales Copilot style)
- **Função:** Sugerir respostas para mensagens de pacientes, filtrar o que precisa de atenção humana
- **IA:** LLM para geração + classificador barato (JEV/OPE) para triagem
- **Inspiração:** Vídeo TypeSafe JEV — usar classificação para baratear chamadas de LLM
- **Status:** 🟡 Em planejamento — inspiração do vídeo JEV

### 4. Agente de Análise de Lead/Conversion
- **Função:** Analisar conversas de WhatsApp, classificar leads por temperatura (quente, morno, frio)
- **IA:** Classificação (sim/não/score) — ideal para JEV ou similar
- **Status:** 🟢 Ideia — validar após implementar agentes 1-3

## Arquitetura proposta

```
Paciente envia WhatsApp → WAHA → DeskcommCRM App
                                       ↓
                          [ Filtro de classificação barato (JEV/OPE) ]
                                       ↓
                    ┌─────────────────┴─────────────────┐
                    ↓ (precisa de atenção)              ↓ (automático)
            LLM gera resposta sugerida           Ação direta (lembrete, etc.)
                    ↓
            Equipe revise/aceite/no envia
```

## JEV (TypeSafe) como classificador barato

Pelo vídeo de 2026-09-20:
- JEV não é LLM — é classificador/decisão
- Latência: ~300-550ms (vs 3s de LLM)
- Custo: absurdamente baixo (R$5 vs R$20-30 projetado por closer)
- Casos de uso: classificação de leads, resposta preparada (sim/não/choice/score)
- Estado: **weightlist** — acesso via OpenRouter (instável para produção)

**Decisão:** Para o MVP do consultório, usar LLM existente (OpenRouter/Anthropic). Explorar JEV como classificador quando estiver disponível e estável.

## Status geral dos agentes

| Agente | Prioridade | Dependências | Status |
|---|---|---|---|
| Agendamento (Google Calendar) | 🔴 Alta | Google Calendar API keys | 🔴 Pendente |
| Follow-up de pacientes | 🟡 Média | WAHA + Supabase (já pronto) | 🟡 Planejamento |
| Respostas WhatsApp (copilot) | 🟡 Média | LLM + WAHA (pronto) | 🟡 Planejamento |
| Análise de leads (classificação) | 🟢 Baixa | Classificador (JEV ou LLM) | 🟢 Ideia |
