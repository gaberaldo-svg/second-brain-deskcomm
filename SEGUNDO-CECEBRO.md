# Segundo Cerebro — Este Repositório

## Propósito

Este repositório (`second-brain-deskcomm`) é o **segundo cérebro** do projeto DeskcommCRM. Ele centraliza todo o contexto necessário para:

1. **Eu entender** o estado atual do projeto sem depender de memória
2. **Um agente automático (cron)** avaliar andamento e sugerir próximos passos
3. **Qualquer pessoa** (futuro eu, colaborador, cliente) entender o projeto de cara

## Por que um segundo cérebro

Projetos de infraestrutura se acumulam contexto: decisões, chaves, integracoes, erros resolvidos, próximos passos. Sem documentacao central, esse conhecimento vive na cabeça ou no chat — e se perde quando o contexto é esquecido ou a sessao muda.

Este repositorio resolve isso: **toda decisao, todo estado, toda tarefa vai aqui.**

## Como usar

### Para o projetista (eu)
- Antes de tomar uma decisao, ler os documentos relevantes
- Após tomar uma decisao, atualizar `DECISOES.md`
- Após configurar algo, atualizar o documento de configuracao correspondente
- Semanalmente, verificar `PENDING-TASKS.md` e ritir tarefas concluídas

### Para o agente de checkpoint (cron)
- Ler `PENDING-TASKS.md`, `CONFIGURACAO-DESKCOMMCRM.md`, `INFRASTRUCTURE.md`
- Comparar estado documentado vs estado real (via SSH ao VPS)
- Sugerir próximos passos e atualizar `PENDING-TASKS.md`

### Para o agente de manutencao do Second Brain
- Verificar se os documentos refletem o estado real do sistema
- Sugerir melhorias na estrutura do repositorio
- Identificar informacoes faltando ou desatualizadas

## Estrutura

```
second-brain-deskcomm/
├── README.md                    # Visao geral e indice
├── INFRASTRUCTURE.md            # VPS, Docker, network, ports
├── OMNIROUTE.md                 # AI Gateway, providers, status
├── CONFIGURACAO-DESKCOMMCRM.md  # .env breakdown, o que falta
├── CHAVES-API-NECESSARIAS.md    # Chaves needed (sem valores)
├── INTEGRACOES.md               # Google Calendar, WAHA, Supabase, etc.
├── IA-AGENTS.md                 # Agentes de IA planejados
├── PENDING-TASKS.md             # Tarefas pendentes (priorizadas)
├── DECISOES.md                  # Log de decisoes
├── CRON-JOBS.md                 # Cron jobs configurados
└── VENDA-E-LANÇAMENTO.md        # Estrategia de venda do servico
```

## Manutencao

Este repositorio e mantido pelo agente de **Manutencao do Second Brain** (cron semanal) e por mim, sempre que uma mudanca significativa ocorre no projeto.
