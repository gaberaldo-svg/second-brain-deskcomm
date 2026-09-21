# OmniRoute — AI Gateway

## Status

|- **Versão:** v3.8.50
|- **Processo:** PM2 (id 0, nome `omniroute`), online, pid 33002, uptime 3D, 39.1MB, root
|- **Porta:** 20128
|- **Data dir:** `/root/.omniroute/` — database 5.8 MB
|- **Config dir:** `/root/.omniroute/` — existe `.env` e `storage.sqlite` (verificado 2026-09-21)

## Providers ativos

| ID | Nome | Namespace | Status |
|---|---|---|---|
| 8e203bde | codestral | main | active |
| 11cad3c2 | g4f-pollinations | main | active |
| ee54511d | gemini | main | active |
| 7becee70 | groq | main | active |
| 3cee386d | huggingface | main | active |
| 35aea43b | kiro | kiro | active |
| 7f02e1e8 | mistral | main | active |
| 48f0f30e | nvidia | main | active |
| 6d00136f | opencode | opencode | active |
| 75d4dbfb | openrouter | main | active |

## Hermes Agent

- Installado via pip: Hermes Agent v0.19.0
- Python 3.11.13, OpenAI SDK 2.24.0
- Integrado ao OmniRoute como CLI tool

## Kiro AI

- **NÃO instalado** — pendência para ter um provider de IA completo

## CLI Tools faltando

Claude Code, Codex CLI, ZCode, Factory Droid, OpenClaw, Cursor, Cline, Kilo Code, Continue, Antigravity, GitHub Copilot, OpenCode, Qwen Code, Aider, e diversos outros — **não são críticos para o MVP**, mas podem ser adicionados futuramente.

## Arquivos de configuração

- `/root/.omniroute/.env` — ambiente do OmniRoute
- `/usr/lib/node_modules/omniroute/.env` — ambiente (STORAGE_ENCRYPTION_KEY ignorado em favor do de /root)

## AÇÃO NECESSÁRIA

1. **Configurar providers com API keys válidas** — alguns providers podem estar sem chave funcional
2. **Instalar Kiro AI** (se desejado) para completar o ecossistema
3. **Verificar se OmniRoute está respondendo** na porta 20128
4. **Configurar o dashboard/TUI do OmniRoute** para gerenciar providers (requer acesso SSH interativo como usuário `hermes`)
