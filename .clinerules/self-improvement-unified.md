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
