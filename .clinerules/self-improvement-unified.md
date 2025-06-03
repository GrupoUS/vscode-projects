---
description: Diretrizes unificadas para aprimorar continuamente as regras do Cline com base em padrões de código emergentes e melhores práticas.
globs: **/*
alwaysApply: true
---

# Auto-Melhoria Unificada do Sistema

Este documento consolida as diretrizes para aprimorar continuamente as regras do Cline, baseando-se em padrões de código emergentes e melhores práticas, combinando insights de `self_improve.mdc`, `.windsurfrules` e `.clinerules/master_rule.md`.

## Gatilhos de Melhoria de Regras:

-   Novos padrões de código não cobertos por regras existentes.
-   Implementações similares repetidas em múltiplos arquivos.
-   Padrões de erro comuns que poderiam ser prevenidos.
-   Novas bibliotecas ou ferramentas sendo usadas consistentemente.
-   Melhores práticas emergentes na base de código.

## Processo de Análise:

-   Comparar novo código com regras existentes.
-   Identificar padrões que devem ser padronizados.
-   Procurar referências à documentação externa.
-   Verificar padrões consistentes de tratamento de erro.
-   Monitorar padrões de teste e cobertura.

## Atualizações de Regras:

-   **Adicionar Novas Regras Quando:**
    -   Uma nova tecnologia/padrão é usado em 3+ arquivos.
    -   Bugs comuns poderiam ser prevenidos por uma regra.
    -   Revisões de código mencionam repetidamente o mesmo feedback.
    -   Novos padrões de segurança ou desempenho emergem.

-   **Modificar Regras Existentes Quando:**
    -   Melhores exemplos existem na base de código.
    -   Casos extremos adicionais são descobertos.
    -   Regras relacionadas foram atualizadas.
    -   Detalhes de implementação mudaram.

## Classificação de Insights
Após identificar um gap, classifique o insight de acordo com o impacto e a urgência:
- **CRÍTICO**: Previne erros que quebram funcionalidade, causam perda de dados ou impactam segurança.
- **IMPORTANTE**: Melhora eficiência significativamente (>20%), reduz retrabalho ou aprimora UX.
- **OTIMIZAÇÃO**: Refinamentos que agregam valor marginal, melhorias de performance menores ou legibilidade.
- **EXPERIMENTAL**: Ideias para teste futuro, conceitos novos ou abordagens não comprovadas.

## Templates Estruturados para Sugestões
Para garantir consistência e clareza nas propostas de melhoria, utilize os seguintes templates:

##### Template: Nova Regra Proposta
```markdown
## Proposta de Nova Regra para .clinerules

**Categoria**: [Técnica/Processo/Ferramenta/UX/Segurança/Performance]
**Prioridade**: [CRÍTICO/IMPORTANTE/OTIMIZAÇÃO/EXPERIMENTAL]
**Trigger Identificado**: [Descreva a situação específica ou o padrão de atrito que ativou esta sugestão. Ex: "Erro recorrente ao configurar ambiente", "Padrão de código duplicado em 3+ arquivos"]
**Problema Resolvido**: [Explique claramente o problema que esta nova regra visa resolver ou o atrito que ela previne. Seja conciso e direto.]
**Regra Proposta**:
```markdown
---
description: [Descrição clara de uma linha do que a regra enforce]
globs: [path/to/files/*.ext, other/path/**/*]
alwaysApply: [true/false]
---

- **[Ponto Principal em Negrito]**
  - [Sub-ponto com detalhes]
  - [Exemplos e explicações]
```
**Justificativa**: [Explique por que esta regra é necessária e como ela melhorará futuros desenvolvimentos. Mencione o impacto esperado (ex: redução de X% de erros, aumento de Y% na eficiência, padronização de Z).]
**Impacto Esperado**: [Métrica ou benefício mensurável. Ex: "Redução de 30% no tempo de setup", "Eliminação de bugs de tipo X", "Melhora na legibilidade do código."]
**Localização Sugerida**: [Caminho completo do arquivo onde a regra deve ser adicionada ou modificada. Ex: `.clinerules/workflows/new-feature-workflow.md`]
```

##### Template: Melhoria de Workflow Existente
```markdown
## Proposta de Melhoria para Workflow Existente

**Workflow Afetado**: [Nome do workflow ou protocolo. Ex: "DEV_WORKFLOW", "Error Handling Protocol"]
**Prioridade**: [CRÍTICO/IMPORTANTE/OTIMIZAÇÃO/EXPERIMENTAL]
**Trigger Identificado**: [Descreva a situação específica ou o atrito que ativou esta sugestão. Ex: "Passos manuais excessivos", "Falta de clareza em uma etapa"]
**Problema Resolvido**: [Explique claramente o problema que esta melhoria visa resolver. Ex: "Retrabalho devido a inconsistências", "Atraso na entrega de tarefas"]
**Melhoria Proposta**: [Descreva a mudança específica no workflow. Pode ser um novo passo, uma automação, uma reordenação de etapas, etc.]
**Justificativa**: [Explique por que esta melhoria é necessária e como ela otimizará o processo. Mencione o impacto esperado.]
**Impacto Esperado**: [Métrica ou benefício mensurável. Ex: "Redução de 15% no tempo de execução do workflow", "Aumento da confiabilidade do processo."]
**Localização Sugerida**: [Caminho completo do arquivo onde a melhoria deve ser documentada. Ex: `.clinerules/workflows/dev-workflow-unified.md`]
```

##### Template: Otimização de Ferramenta/MCP
```markdown
## Proposta de Otimização para Ferramenta/MCP

**Ferramenta/MCP Afetada**: [Nome da ferramenta ou servidor MCP. Ex: "sequentialthinking", "Taskmaster CLI", "Figma-Context-MCP"]
**Prioridade**: [CRÍTICO/IMPORTANTE/OTIMIZAÇÃO/EXPERIMENTAL]
**Trigger Identificado**: [Descreva a situação específica ou o atrito que ativou esta sugestão. Ex: "Uso ineficiente da ferramenta", "Falta de integração com outro sistema"]
**Problema Resolvido**: [Explique claramente o problema que esta otimização visa resolver. Ex: "Custo elevado de tokens", "Tempo de resposta lento", "Funcionalidade não explorada"]
**Otimização Proposta**: [Descreva a mudança específica na configuração ou uso da ferramenta/MCP. Pode ser um novo parâmetro, uma forma de uso mais eficiente, uma integração.]
**Justificativa**: [Explique por que esta otimização é necessária e como ela melhorará o desempenho ou custo. Mencione o impacto esperado.]
**Impacto Esperado**: [Métrica ou benefício mensurável. Ex: "Redução de 20% no custo de tokens", "Aumento de 10% na velocidade de execução", "Melhora na precisão da IA."]
**Localização Sugerida**: [Caminho completo do arquivo onde a otimização deve ser documentada. Ex: `.clinerules/sequential-thinking-mcp.md`, `.clinerules/00-cost-optimization.md`]
```

## Exemplo de Reconhecimento de Padrão:

```typescript
// Se você vir padrões repetidos como:
const data = await prisma.user.findMany({
  select: { id: true, email: true },
  where: { status: 'ACTIVE' }
});

// Considere adicionar uma seção PRISMA em .clinerules/tooling/prisma-rules.md (exemplo):
// - Campos de seleção padrão
// - Condições where comuns
// - Padrões de otimização de desempenho
```

## Verificações de Qualidade de Regras:

-   As regras devem ser acionáveis e específicas.
-   Os exemplos devem vir de código real.
-   As referências devem estar atualizadas.
-   Os padrões devem ser aplicados consistentemente.

## Melhoria Contínua:

-   Monitorar comentários de revisão de código.
-   Rastrear perguntas comuns de desenvolvimento.
-   Atualizar regras após grandes refatorações.
-   Adicionar links para documentação relevante.
-   Fazer referência cruzada a regras relacionadas.

## Depreciação de Regras:

-   Marcar padrões desatualizados como depreciados.
-   Remover regras que não se aplicam mais.
-   Atualizar referências a regras depreciadas.
-   Documentar caminhos de migração para padrões antigos.

## Atualizações de Documentação:

-   Manter exemplos sincronizados com o código.
-   Atualizar referências a documentos externos.
-   Manter links entre regras relacionadas.
-   Documentar mudanças que quebram a compatibilidade.

Siga as diretrizes de formatação de regras em [`cursor-rules.md`](.clinerules/tooling/cursor-rules.md) para a estrutura adequada das seções de regras.
