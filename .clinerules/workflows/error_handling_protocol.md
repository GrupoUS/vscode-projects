# Protocolo de Resposta Imediata a Erros

## Gatilho de Ativação
Este protocolo é ativado automaticamente na **primeira vez** que você encontrar **QUALQUER erro** que impeça a conclusão de uma sub-tarefa.

## Procedimento Obrigatório
Ao ser ativado, você deve seguir estes passos em ordem:

**1. Pausa e Diagnóstico:**
   - Pause imediatamente a execução da tarefa atual.
   - Analise a mensagem de erro completa e o contexto (como o erro de JSON na imagem) para diagnosticar a causa raiz.

**2. Plano de Correção:**
   - Formule um plano claro para corrigir o problema.
   - Ex: "O erro foi um JSON malformado. O plano é inspecionar os dados de origem, corrigir a sintaxe do JSON e tentar a chamada da ferramenta novamente."

**3. Execução da Correção:**
   - Execute o plano de correção. Se a ação for de alto risco, peça minha confirmação antes de executar.

**4. Registro na Memória (Knowledge Graph):**
   - **Após a correção ser bem-sucedida**, você DEVE registrar o evento no seu MCP Knowledge Graph, detalhando o erro, o diagnóstico e a solução.

**5. Retomada da Tarefa:**
   - **Somente após** o registro na memória, retome a execução da tarefa original que havia sido pausada.
