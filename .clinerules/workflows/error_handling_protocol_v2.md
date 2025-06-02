# Protocolo de Tratamento de Erros e Auto-Correção (Versão Complementar)

## Protocolo Base (Já Implementado)
O protocolo principal em `error_handling_protocol.md` permanece ativo para resposta imediata a erros críticos.

## Protocolo Complementar: Regra das 2 Tentativas

### Gatilho de Ativação
Este protocolo complementar é ativado quando você encontrar o **mesmo erro específico** por **2 (duas) ou mais vezes consecutivas** ao tentar executar uma única sub-tarefa.

### Procedimento Obrigatório
Ao ser ativado, você deve seguir estes passos em ordem:

**1. Pausa e Diagnóstico Aprofundado:**
   - Pause imediatamente a execução da tarefa atual.
   - Analise a mensagem de erro completa e o contexto para diagnosticar a causa raiz do problema (ex: permissão negada, diretório inexistente, comando inválido, falha de API).
   - Compare com tentativas anteriores para identificar padrões.

**2. Plano de Correção Sistemática:**
   - Formule um plano claro e conciso para corrigir o problema.
   - Exemplos:
     - *Erro de permissão:* Tentar executar o comando com `sudo`.
     - *Diretório não encontrado:* Criar o diretório necessário com `mkdir -p`.
     - *Comando inválido:* Consultar a documentação para corrigir a sintaxe do comando.
     - *Falha de API/MCP:* Verificar conectividade, credenciais ou tentar método alternativo.

**3. Execução da Correção:**
   - Execute o plano de correção. Se a ação for de alto risco (ex: alterar permissões de arquivos de sistema), peça confirmação antes de executar.

**4. Registro na Memória (Knowledge Graph):**
   - **Após a correção ser bem-sucedida**, você DEVE registrar o evento no seu MCP Knowledge Graph.
   - O registro deve incluir:
     - Um nó de `Erro` com a mensagem original.
     - Um nó de `Diagnóstico` com a causa raiz que você identificou.
     - Um nó de `Ação Corretiva` com o comando ou passo que você executou para resolver.
     - As devidas relações entre esses nós.

**5. Retomada da Tarefa:**
   - **Somente após** o registro na memória ser concluído, retome a execução da tarefa original que havia sido pausada.

## Integração com Protocolo Principal
- O protocolo principal (`error_handling_protocol.md`) continua ativo para erros críticos imediatos
- Este protocolo complementar atua especificamente para erros recorrentes
- Ambos utilizam o mesmo sistema de Knowledge Graph para aprendizado contínuo

## Hierarquia de Ativação
1. **Erro Crítico Imediato** → Protocolo Principal
2. **Erro Recorrente (2+ vezes)** → Protocolo Complementar
3. **Ambos registram no Knowledge Graph** para aprendizado futuro
