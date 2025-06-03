---
description: Protocolo coordenador central do sistema .clinerules com hierarquia de precedência e workflows obrigatórios
author: Sistema GRUPOUS/Cline Rules
version: 2.0
globs: ["**/*"]
tags: ["master", "coordinator", "protocol", "mandatory", "high-priority"]
alwaysApply: true
---

# Master Rule - Protocolo Coordenador Central do Sistema .clinerules

## 🚨 DIRETIVA PRINCIPAL: PROTOCOLO OBRIGATÓRIO DE 4 CAMADAS

Este arquivo implementa o **PROTOCOLO UNIFICADO** definido em `.clinerules/unified-protocol.md` que **DEVE** ser executado em TODA tarefa, garantindo continuidade de contexto, aprendizado contínuo, meta-melhoria e verificação sistemática.

✅ **EXECUÇÃO OBRIGATÓRIA**: As 4 camadas do protocolo unificado **DEVEM** ser executadas em SEQUÊNCIA para toda tarefa não-trivial.

### Estrutura Macro Obrigatória (referência: unified-protocol.md)
1. **Layer 1**: Memory Foundation (carregar contexto completo) - **🔄 Com feedback visual obrigatório**
2. **Layer 2**: Meta-Improvement Protocol (sugestões de melhoria) - **🔍 Critérios expandidos + ativação manual**
3. **Layer 3**: Completeness Verification (verificar completude) - **✅ Com feedback visual obrigatório**
4. **Layer 4**: Post-Task Learning (capturar conhecimento) - **📚 Com feedback visual obrigatório**

### Funcionalidades Expandidas
- **Feedback Visual**: Cada layer anuncia seu início com emojis e mensagens claras
- **Ativação Manual**: Usuário pode digitar `!reflect` para forçar Layer 2 em qualquer momento
- **Sensibilidade Aumentada**: Layer 2 ativa em mais situações (+ de 2 arquivos, + de 5 min, qualquer feedback)

**Para detalhes completos das 4 camadas, consulte `.clinerules/unified-protocol.md`**

---

## WORKFLOWS ESPECÍFICOS E COORDENAÇÃO

### Sequência de Execução Refinada
Siga esta sequência obrigatória em todas as operações:

### Passo 1: Verificação de Contexto Local
- Sempre verifique se existe um sistema de regras local (`.ai_memory/master_rule.md`)
- Se existir, as regras locais têm precedência absoluta sobre estas regras globais
- Se não existir, proceda com os protocolos definidos neste sistema

### Passo 2: Análise da Tarefa
- Analise a tarefa solicitada pelo usuário
- **Avalie a complexidade**: Se a tarefa requer análise multi-etapa, considere usar `sequential-thinking-mcp.md`
- Identifique qual workflow específico deve ser aplicado
- Consulte os arquivos de workflow relevantes em `.clinerules/workflows/`
- **Ferramentas MCP**: Ative ferramentas especializadas conforme critérios definidos em suas regras específicas

### Passo 3: Executar Conforme o Plano
- Execute a tarefa seguindo o workflow identificado
- **IMPORTANTE**: Durante a execução, monitore os erros ativamente
- **Na primeira ocorrência de qualquer erro que impeça a conclusão de uma sub-tarefa**, pause a tarefa imediatamente e ative o `error_handling_protocol.md` antes de prosseguir
- Mantenha registro de todas as ações e decisões tomadas

### Passo 4: Verificação de Completude (OBRIGATÓRIO)
- **ANTES** de considerar qualquer tarefa como finalizada:
  - **Altere para PLAN MODE** para executar verificação
  - **Execute** o protocolo definido em `completude-verification-protocol.md`
  - **Compare** planejamento inicial vs execução realizada
  - **Identifique** gaps críticos, importantes e opcionais
  - **Crie plano** de completude se necessário
  - **Resolva gaps críticos** antes de finalizar
- **Só após verificação**: Prossiga com `attempt_completion`

### Passo 5: Protocolo de Melhoria Contínua
- Após completar qualquer tarefa, reflita sobre:
  - Erros encontrados e como foram resolvidos
  - Padrões que emergiram durante a execução
  - Oportunidades de melhoria nos protocolos existentes
- Registre aprendizados no MCP Knowledge Graph quando aplicável
- Atualize protocolos conforme necessário seguindo `self_improve.md`

## Workflows e Ferramentas Disponíveis

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

### Pensamento Sequencial (MCP Tool)
- **Arquivo**: `.clinerules/sequential-thinking-mcp.md`
- **Uso**: Para resolução de problemas complexos que requerem análise multi-etapa
- **Ativação**: Automática para problemas de arquitetura, debugging complexo, planejamento estratégico
- **Integração**: Ferramenta MCP sequentialthinking para pensamento iterativo e reflexivo

### Verificação de Completude
- **Arquivo**: `.clinerules/completude-verification-protocol.md`
- **Uso**: Verificação obrigatória de que todas as tarefas foram 100% completadas
- **Ativação**: Automática antes de finalizar qualquer tarefa complexa
- **Integração**: Coordena com error_handling e exige PLAN MODE para verificação

### Auto-Melhoria
- **Arquivo**: Referenciado nas regras globais como `self_improve.md`
- **Uso**: Para evolução contínua dos protocolos e regras
- **Aplicação**: Após cada tarefa significativa

## Hierarquia de Precedência Atualizada

1. **Regras Locais** (`.ai_memory/master_rule.md`) - Precedência absoluta
2. **Protocolo Unificado** (`unified-protocol.md`) - Estrutura obrigatória de 4 camadas
3. **Protocolos de Emergência** (`error_handling_protocol.md`) - Ativação automática
4. **Ferramentas MCP Especializadas** (`sequential-thinking-mcp.md`) - Para problemas complexos
5. **Workflows Específicos** (arquivos em `.clinerules/workflows/`)
6. **Regras Globais** (sistema base)

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

---

## REGRAS CONSOLIDADAS DO SISTEMA DE DESENVOLVIMENTO

### Workflow de Desenvolvimento (DEV_WORKFLOW)
**Descrição**: Guia para usar scripts de meta-desenvolvimento para gerenciar workflows de desenvolvimento orientados a tarefas.

#### Comandos CLI Globais
- Task Master fornece uma CLI global através do comando `task-master`
- Toda funcionalidade de `scripts/dev.js` disponível através desta interface
- Instalar globalmente com `npm install -g claude-task-master` ou usar localmente via `npx`
- Usar `task-master <command>` em vez de `node scripts/dev.js <command>`
- Exemplos:
  - `task-master list` em vez de `node scripts/dev.js list`
  - `task-master next` em vez de `node scripts/dev.js next`
  - `task-master expand --id=3` em vez de `node scripts/dev.js expand --id=3`
- Todos os comandos aceitam as mesmas opções que seus equivalentes de script
- A CLI fornece comandos adicionais como `task-master init` para configuração de projeto

#### Processo de Workflow de Desenvolvimento
- Iniciar novos projetos executando `task-master init` ou `node scripts/dev.js parse-prd --input=<prd-file.txt>` para gerar tasks.json inicial
- Começar sessões de codificação com `task-master list` para ver tarefas atuais, status e IDs
- Analisar complexidade das tarefas com `task-master analyze-complexity --research` antes de decompor tarefas
- Selecionar tarefas baseado em dependências (todas marcadas como 'done'), nível de prioridade e ordem de ID
- Esclarecer tarefas verificando arquivos de tarefa no diretório tasks/ ou perguntando ao usuário
- Ver detalhes específicos da tarefa usando `task-master show <id>` para entender requisitos de implementação
- Decompor tarefas complexas usando `task-master expand --id=<id>` com flags apropriadas
- Limpar subtarefas existentes se necessário usando `task-master clear-subtasks --id=<id>` antes de regenerar
- Implementar código seguindo detalhes da tarefa, dependências e padrões do projeto
- Verificar tarefas de acordo com estratégias de teste antes de marcar como completa
- Marcar tarefas completadas com `task-master set-status --id=<id> --status=done`
- Atualizar tarefas dependentes quando implementação difere do plano original
- Gerar arquivos de tarefa com `task-master generate` após atualizar tasks.json
- Manter estrutura de dependência válida com `task-master fix-dependencies` quando necessário
- Respeitar cadeias de dependência e prioridades de tarefa ao selecionar trabalho
- Reportar progresso regularmente usando o comando list

### Diretrizes para Criação de Regras (WINDSURF_RULES)
**Descrição**: Diretrizes para criar e manter regras para garantir consistência e efetividade.

#### Estrutura de Regra Obrigatória
```markdown
---
description: Descrição clara de uma linha do que a regra enforce
globs: path/to/files/*.ext, other/path/**/*
alwaysApply: boolean
---

- **Pontos Principais em Negrito**
  - Sub-pontos com detalhes
  - Exemplos e explicações
```

#### Referências de Seção
- Usar `ALL_CAPS_SECTION` para referenciar arquivos
- Exemplo: `WINDSURF_RULES`

#### Exemplos de Código
- Usar blocos de código específicos da linguagem
```typescript
// ✅ FAÇA: Mostrar exemplos bons
const goodExample = true;

// ❌ NÃO FAÇA: Mostrar anti-padrões
const badExample = false;
```

#### Diretrizes de Conteúdo de Regras
- Começar com visão geral de alto nível
- Incluir requisitos específicos e acionáveis
- Mostrar exemplos de implementação correta
- Referenciar código existente quando possível
- Manter regras DRY referenciando outras regras

#### Manutenção de Regras
- Atualizar regras quando novos padrões emergirem
- Adicionar exemplos do codebase atual
- Remover padrões obsoletos
- Cross-referenciar regras relacionadas

#### Melhores Práticas
- Usar bullet points para clareza
- Manter descrições concisas
- Incluir exemplos de FAÇA e NÃO FAÇA
- Referenciar código real em vez de exemplos teóricos
- Usar formatação consistente entre regras

### Auto-Melhoria do Sistema (SELF_IMPROVE)
**Descrição**: Diretrizes para melhorar continuamente este documento de regras baseado em padrões de código emergentes e melhores práticas.

#### Gatilhos de Melhoria de Regras
- Novos padrões de código não cobertos por regras existentes
- Implementações similares repetidas em múltiplos arquivos
- Padrões de erro comuns que poderiam ser prevenidos
- Novas bibliotecas ou ferramentas sendo usadas consistentemente
- Melhores práticas emergentes no codebase

#### Processo de Análise
- Comparar novo código com regras existentes
- Identificar padrões que devem ser padronizados
- Procurar referências à documentação externa
- Verificar padrões consistentes de tratamento de erro
- Monitorar padrões de teste e cobertura

#### Atualizações de Regras
**Adicionar Novas Regras Quando:**
- Uma nova tecnologia/padrão é usado em 3+ arquivos
- Bugs comuns poderiam ser prevenidos por uma regra
- Code reviews mencionam repetidamente o mesmo feedback
- Novos padrões de segurança ou performance emergem

**Modificar Regras Existentes Quando:**
- Melhores exemplos existem no codebase
- Casos extremos adicionais são descobertos
- Regras relacionadas foram atualizadas
- Detalhes de implementação mudaram

#### Verificações de Qualidade de Regras
- Regras devem ser acionáveis e específicas
- Exemplos devem vir de código real
- Referências devem estar atualizadas
- Padrões devem ser consistentemente enforced

#### Melhoria Contínua
- Monitorar comentários de code review
- Rastrear questões comuns de desenvolvimento
- Atualizar regras após refatorações maiores
- Adicionar links para documentação relevante
- Cross-referenciar regras relacionadas

#### Depreciação de Regras
- Marcar padrões obsoletos como deprecated
- Remover regras que não se aplicam mais
- Atualizar referências a regras deprecated
- Documentar caminhos de migração para padrões antigos

#### Atualizações de Documentação
- Manter exemplos sincronizados com código
- Atualizar referências a documentação externa
- Manter links entre regras relacionadas
- Documentar breaking changes
