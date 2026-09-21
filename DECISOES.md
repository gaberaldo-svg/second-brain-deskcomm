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
