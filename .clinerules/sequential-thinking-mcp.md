---
description: Guia para uso efetivo da ferramenta sequentialthinking MCP para resolução de problemas complexos
author: Sistema GRUPOUS/Cline Rules
version: 2.0
globs: ["**/*"]
tags: ["sequential-thinking", "mcp-tool", "problem-solving", "complex-analysis", "mandatory"]
alwaysApply: true
---

# Sequential Thinking MCP - Guia de Uso Avançado

Esta regra define o protocolo obrigatório para utilização da ferramenta `sequentialthinking` MCP, uma ferramenta especializada em resolução de problemas complexos através de pensamento iterativo, reflexivo e sequencial.

## 1. Objetivo e Filosofia

### Missão da Ferramenta
A ferramenta `sequentialthinking` é projetada para enfrentar problemas que requerem:
- **Decomposição de complexidade**: Quebrar problemas grandes em etapas menores
- **Pensamento adaptativo**: Ajustar a abordagem conforme novas informações emergem
- **Reflexão sistemática**: Questionar e revisar decisões anteriores
- **Manutenção de contexto**: Preservar o fio condutor do raciocínio ao longo de múltiplas etapas

### Quando NÃO Usar
**CRÍTICO**: Não use esta ferramenta para:
- Tarefas simples de uma única etapa
- Perguntas diretas com respostas óbvias
- Operações rotineiras de código
- Busca de informações básicas

## 2. Critérios de Ativação Obrigatórios

Use a ferramenta `sequentialthinking` quando enfrentar:

### 2.1. Problemas de Arquitetura e Design
- Planejamento de novas features complexas
- Refatoração de sistemas com múltiplas dependências
- Decisões arquiteturais que afetam múltiplos módulos
- Migração entre tecnologias ou frameworks

### 2.2. Debugging e Análise Complexa
- Bugs que envolvem múltiplas camadas do sistema
- Problemas de performance com causas não óbvias
- Conflitos de dependências ou versões
- Análise de logs complexos ou traces de erro

### 2.3. Planejamento e Estratégia
- Definição de roadmaps de desenvolvimento
- Análise de impacto de mudanças
- Priorização de tarefas com múltiplas variáveis
- Estimativas de projetos com incertezas

### 2.4. Resolução de Problemas Multicontextuais
- Integração entre diferentes sistemas
- Problemas que requerem conhecimento de múltiplas tecnologias
- Decisões que afetam UX, performance e segurança simultaneamente

## 3. Protocolo de Uso - Sintaxe e Parâmetros

### 3.1. Sintaxe Base
```javascript
use_mcp_tool(
  'github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking',
  'sequentialthinking',
  {
    "thought": "string_required",
    "nextThoughtNeeded": boolean_required,
    "thoughtNumber": integer_required_min_1,
    "totalThoughts": integer_required_min_1,
    "isRevision": boolean_optional,
    "revisesThought": integer_optional_min_1,
    "branchFromThought": integer_optional_min_1,
    "branchId": "string_optional",
    "needsMoreThoughts": boolean_optional
  }
)
```

### 3.2. Parâmetros Detalhados

#### Parâmetros Obrigatórios
- **`thought`**: O conteúdo atual do pensamento. Deve ser específico, claro e focado
- **`nextThoughtNeeded`**: `true` se mais pensamentos são necessários, `false` APENAS quando concluído
- **`thoughtNumber`**: Número sequencial do pensamento atual (começar em 1)
- **`totalThoughts`**: Estimativa atual do total de pensamentos necessários (ajustável)

#### Parâmetros Opcionais
- **`isRevision`**: `true` quando este pensamento revisa um anterior
- **`revisesThought`**: Número do pensamento sendo revisado (use com `isRevision: true`)
- **`branchFromThought`**: Número do pensamento de onde uma nova linha de raciocínio se origina
- **`branchId`**: Identificador para a branch atual (ex: "alternative_approach", "security_analysis")
- **`needsMoreThoughts`**: `true` quando atingir `totalThoughts` mas perceber que precisa de mais

## 4. Workflow Iterativo - Boas Práticas

### 4.1. Estrutura de Início
```javascript
// Thought 1: Sempre começar com análise inicial
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Analisando o problema: [descrição específica]. Identifico os componentes principais: A, B, C. Minha abordagem inicial será...",
  "nextThoughtNeeded": true,
  "thoughtNumber": 1,
  "totalThoughts": 5  // Estimativa inicial conservadora
})
```

### 4.2. Padrões de Progressão

#### Pensamento Sequencial Normal
```javascript
// Thought 2: Aprofundando
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Aprofundando o componente A: Descobri que há uma dependência com X que não havia considerado...",
  "nextThoughtNeeded": true,
  "thoughtNumber": 2,
  "totalThoughts": 5
})
```

#### Revisão de Pensamento Anterior
```javascript
// Thought 3: Revisando decisão anterior
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Revisando minha análise do Thought 1: A abordagem inicial não considera o aspecto Y. Ajustando para...",
  "nextThoughtNeeded": true,
  "thoughtNumber": 3,
  "totalThoughts": 6,  // Ajustado para cima
  "isRevision": true,
  "revisesThought": 1
})
```

#### Ramificação de Análise
```javascript
// Thought 4: Explorando alternativa
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Explorando abordagem alternativa baseada no Thought 2: Em vez de X, poderíamos usar Z...",
  "nextThoughtNeeded": true,
  "thoughtNumber": 4,
  "totalThoughts": 7,
  "branchFromThought": 2,
  "branchId": "alternative_approach"
})
```

#### Percebendo Necessidade de Mais Pensamentos
```javascript
// Thought 5: Descobrindo complexidade adicional
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Chegando ao pensamento 5 de 5, mas percebo que há aspectos de segurança que não analisei...",
  "nextThoughtNeeded": true,
  "thoughtNumber": 5,
  "totalThoughts": 8,  // Aumentando o total
  "needsMoreThoughts": true
})
```

### 4.3. Finalização Adequada
```javascript
// Thought Final: Conclusão e verificação
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Solução final: Após análise completa, a abordagem recomendada é... Esta solução atende aos critérios X, Y, Z e foi validada contra as alternativas consideradas.",
  "nextThoughtNeeded": false,  // APENAS quando verdadeiramente concluído
  "thoughtNumber": 8,
  "totalThoughts": 8
})
```

## 5. Exemplos Práticos do Contexto de Desenvolvimento

### 5.1. Exemplo: Planejamento de Feature de Autenticação

```javascript
// Cenário: Implementar sistema de autenticação multi-fator

// Thought 1
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Planejando sistema de autenticação multi-fator. Componentes identificados: 1) Backend auth service, 2) Frontend UI components, 3) Database schema, 4) Integration com providers externos. Começarei analisando o backend.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 1,
  "totalThoughts": 6
})

// Thought 2
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Backend: Supabase Auth já oferece MFA nativo. Preciso verificar: tipos de MFA suportados (TOTP, SMS), configuração de policies, handling de recovery codes. Isso simplifica significativamente a implementação.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 2,
  "totalThoughts": 6
})

// Thought 3
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Frontend: Componentes necessários: 1) MFA setup wizard, 2) Login flow com MFA challenge, 3) Recovery options, 4) Settings para gerenciar MFA. Usando padrão existente do projeto com React + Tailwind.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 3,
  "totalThoughts": 6
})

// Thought 4 - Revisão
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Revisando Thought 1: Esqueci de considerar aspectos de UX/UI para usuários existentes. Como migrar usuários sem MFA? Precisa ser opt-in inicialmente.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 4,
  "totalThoughts": 7,
  "isRevision": true,
  "revisesThought": 1
})

// Thought 5 - Nova análise
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Estratégia de migração: 1) Soft launch apenas para novos usuários, 2) Email campaign educacional para usuários existentes, 3) Dashboard banner com incentivo para ativar MFA, 4) Considerar reward/gamification.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 5,
  "totalThoughts": 7
})

// Thought 6 - Segurança
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Aspectos de segurança: 1) Rate limiting para MFA attempts, 2) Secure storage de recovery codes, 3) Audit logging de eventos MFA, 4) Session management após MFA verification. Supabase RLS cobre a maioria.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 6,
  "totalThoughts": 7
})

// Thought 7 - Finalização
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Plano final: 1) Configure Supabase MFA settings, 2) Implementar MFA UI components, 3) Setup migration strategy gradual, 4) Implement security measures, 5) Testing strategy com diferentes cenários. Pronto para implementação.",
  "nextThoughtNeeded": false,
  "thoughtNumber": 7,
  "totalThoughts": 7
})
```

### 5.2. Exemplo: Debugging de Performance Issue

```javascript
// Cenário: Dashboard carregando lentamente

// Thought 1
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Investigando lentidão no dashboard. Sintomas: load time > 5s, usuários reportando timeout. Possíveis causas: 1) Database queries, 2) Frontend rendering, 3) Network requests, 4) Bundle size. Começando com profiling.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 1,
  "totalThoughts": 5
})

// Thought 2
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Profiling results: Network tab mostra query de 3.2s para /api/dashboard-data. Database é o gargalo. Analisando query: JOIN complexo entre 4 tabelas sem índices adequados.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 2,
  "totalThoughts": 5
})

// Thought 3 - Branch para análise de índices
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Analisando estrutura de índices: Tabela users (10k rows), posts (50k rows), comments (200k rows), likes (500k rows). Query atual usa full table scan. Índices compostos necessários.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 3,
  "totalThoughts": 6,
  "branchFromThought": 2,
  "branchId": "database_optimization"
})

// Thought 4 - Descobrindo problema adicional
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Aguarde, há outro problema: Query está retornando TODOS os posts do usuário, mas dashboard só mostra 10 mais recentes. Overfetching massivo. Duas soluções: índices + LIMIT, ou paginação.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 4,
  "totalThoughts": 7,
  "needsMoreThoughts": true
})

// Thought 5 - Estratégia de otimização
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Estratégia multi-layer: 1) Adicionar índices compostos, 2) Implementar LIMIT na query, 3) Cache no Redis para queries frequentes, 4) Lazy loading para componentes não críticos.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 5,
  "totalThoughts": 7
})

// Thought 6 - Validação da solução
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Testando solução: Índices reduzem query de 3.2s para 0.1s. LIMIT resolve overfetching. Cache adicional pode reduzir para < 0.05s. Total load time esperado: < 1s. Implementação prioritária: índices primeiro.",
  "nextThoughtNeeded": true,
  "thoughtNumber": 6,
  "totalThoughts": 7
})

// Thought 7 - Plano de implementação
use_mcp_tool('...', 'sequentialthinking', {
  "thought": "Plano de implementação: 1) Migration para criar índices (sem downtime), 2) Update query com LIMIT, 3) Deploy e monitoring, 4) Se necessário, implementar cache layer. Solução completa e testável.",
  "nextThoughtNeeded": false,
  "thoughtNumber": 7,
  "totalThoughts": 7
})
```

## 6. Integração com Sistema de Regras

### 6.1. Ativação Automática
Esta regra é ativada automaticamente quando:
- O contexto da tarefa sugere complexidade multi-etapa
- O problema requer análise de múltiplas variáveis
- Há necessidade de explorar alternativas
- A solução inicial precisa de refinamento

### 6.2. Coordenação com Master Rule
- Segue o protocolo definido em `.clinerules/master_rule.md`
- Integra com `error_handling_protocol.md` se necessário
- Registra insights no Knowledge Graph quando aplicável

### 6.3. Monitoramento e Melhoria
- Cada uso deve ser avaliado quanto à efetividade
- Padrões emergentes devem ser documentados
- Aprimoramentos à regra devem seguir `self_improve.md`

## 7. Armadilhas Críticas e Lembretes

### 7.1. NUNCA Faça
- **Não termine prematuramente**: Só use `nextThoughtNeeded: false` quando verdadeiramente concluído
- **Não ignore ajustes**: Sempre ajuste `totalThoughts` conforme necessário
- **Não pule validação**: Cada thought deve ter propósito específico
- **Não ignore contexto**: Mantenha conexão entre thoughts

### 7.2. SEMPRE Faça
- **Incremente corretamente**: `thoughtNumber` deve sempre aumentar
- **Seja específico**: Cada `thought` deve ter foco claro
- **Expresse incerteza**: Se não tem certeza, diga explicitamente
- **Revise quando necessário**: Use `isRevision` para correções

### 7.3. Sinais de Uso Correto
- Cada thought adiciona valor real ao processo
- O raciocínio é claro e sequencial
- Revisões e branches são justificadas
- A conclusão é bem fundamentada

### 7.4. Sinais de Uso Incorreto
- Thoughts repetitivos sem progresso
- Uso para problemas simples
- Falta de conexão entre thoughts
- Conclusão sem validação adequada

## 8. Checklist de Validação

### Antes de Começar
- [ ] O problema é verdadeiramente complexo?
- [ ] Múltiplas etapas de raciocínio são necessárias?
- [ ] Há potencial para revisão e refinamento?

### Durante o Processo
- [ ] Cada thought adiciona insight novo?
- [ ] A numeração está correta?
- [ ] `totalThoughts` reflete a realidade atual?
- [ ] Revisões estão marcadas adequadamente?

### Ao Finalizar
- [ ] A solução foi validada contra o problema original?
- [ ] Alternativas foram consideradas?
- [ ] O raciocínio pode ser seguido por outros?
- [ ] `nextThoughtNeeded: false` é verdadeiramente apropriado?

---

*Esta regra garante o uso consistente e efetivo da ferramenta sequentialthinking para resolução de problemas complexos, mantendo alta qualidade no processo de raciocínio e tomada de decisão.*
