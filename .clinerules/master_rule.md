# Master Rule - Sistema de Coordenação de Protocolos

## Protocolo Principal de Execução

Este é o arquivo mestre que coordena todos os protocolos e workflows do sistema. Siga esta sequência obrigatória em todas as operações:

### Passo 1: Verificação de Contexto Local
- Sempre verifique se existe um sistema de regras local (`.ai_memory/master_rule.md`)
- Se existir, as regras locais têm precedência absoluta sobre estas regras globais
- Se não existir, proceda com os protocolos definidos neste sistema

### Passo 2: Análise da Tarefa
- Analise a tarefa solicitada pelo usuário
- Identifique qual workflow específico deve ser aplicado
- Consulte os arquivos de workflow relevantes em `.clinerules/workflows/`

### Passo 3: Executar Conforme o Plano
- Execute a tarefa seguindo o workflow identificado
- **IMPORTANTE**: Durante a execução, monitore os erros ativamente
- **Na primeira ocorrência de qualquer erro que impeça a conclusão de uma sub-tarefa**, pause a tarefa imediatamente e ative o `error_handling_protocol.md` antes de prosseguir
- Mantenha registro de todas as ações e decisões tomadas

### Passo 4: Protocolo de Melhoria Contínua
- Após completar qualquer tarefa, reflita sobre:
  - Erros encontrados e como foram resolvidos
  - Padrões que emergiram durante a execução
  - Oportunidades de melhoria nos protocolos existentes
- Registre aprendizados no MCP Knowledge Graph quando aplicável
- Atualize protocolos conforme necessário seguindo `self_improve.md`

## Workflows Disponíveis

### Desenvolvimento de Software
- **Arquivo**: `.clinerules/workflows/dev_workflow.md`
- **Uso**: Para tarefas de desenvolvimento, programação e gerenciamento de projetos
- **Integração**: Utiliza Task Master MCP para gerenciamento de tarefas

### Tratamento de Erros
- **Arquivo Principal**: `.clinerules/workflows/error_handling_protocol.md`
- **Arquivo Complementar**: `.clinerules/workflows/error_handling_protocol_v2.md`
- **Uso**: Ativado automaticamente quando erros são detectados
- **Gatilho Principal**: Primeira ocorrência de qualquer erro que impeça a conclusão de uma sub-tarefa
- **Gatilho Complementar**: Mesmo erro específico ocorrendo 2+ vezes consecutivas (Regra das 2 Tentativas)

### Auto-Melhoria
- **Arquivo**: Referenciado nas regras globais como `self_improve.md`
- **Uso**: Para evolução contínua dos protocolos e regras
- **Aplicação**: Após cada tarefa significativa

## Hierarquia de Precedência

1. **Regras Locais** (`.ai_memory/master_rule.md`) - Precedência absoluta
2. **Protocolos de Emergência** (`error_handling_protocol.md`) - Ativação automática
3. **Workflows Específicos** (arquivos em `.clinerules/workflows/`)
4. **Regras Globais** (definidas no sistema base)

## Integração com Knowledge Graph

- Todos os protocolos devem utilizar o MCP Knowledge Graph para:
  - Registrar erros e suas soluções
  - Armazenar padrões identificados
  - Manter histórico de melhorias implementadas
  - Facilitar aprendizado contínuo

## Monitoramento de Erros

Este sistema implementa monitoramento ativo de erros através do `error_handling_protocol.md`. O protocolo é ativado automaticamente e garante:
- Diagnóstico preciso de problemas
- Correção sistemática de erros
- Registro de soluções para referência futura
- Prevenção de loops infinitos de erro
