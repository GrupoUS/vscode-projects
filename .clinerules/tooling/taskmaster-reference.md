---
description: Referência abrangente para ferramentas MCP e comandos CLI do Taskmaster.
globs: **/*
alwaysApply: true
---
# Referência de Ferramentas e Comandos do Taskmaster

Este documento fornece uma referência detalhada para interagir com o Taskmaster, cobrindo tanto as ferramentas MCP recomendadas, adequadas para integrações como o Cursor, quanto os comandos CLI `task-master` correspondentes, projetados para interação direta do usuário ou fallback.

**Nota:** Para interagir com o Taskmaster programaticamente ou via ferramentas integradas, o uso das **ferramentas MCP é fortemente recomendado** devido ao melhor desempenho, dados estruturados e tratamento de erros. Os comandos CLI servem como uma alternativa amigável ao usuário e fallback.

**Importante:** Várias ferramentas MCP envolvem processamento de IA... As ferramentas alimentadas por IA incluem `parse_prd`, `analyze_project_complexity`, `update_subtask`, `update_task`, `update`, `expand_all`, `expand_task` e `add_task`.

---

## Inicialização e Configuração

### 1. Inicializar Projeto (`init`)

*   **Ferramenta MCP:** `initialize_project`
*   **Comando CLI:** `task-master init [opções]`
*   **Descrição:** `Configura a estrutura básica de arquivos e a configuração do Taskmaster no diretório atual para um novo projeto.`
*   **Principais Opções CLI:**
    *   `--name <nome>`: `Define o nome do seu projeto na configuração do Taskmaster.`
    *   `--description <texto>`: `Fornece uma breve descrição para o seu projeto.`
    *   `--version <versão>`: `Define a versão inicial do seu projeto, por exemplo, '0.1.0'.`
    *   `-y, --yes`: `Inicializa o Taskmaster rapidamente usando as configurações padrão sem prompts interativos.`
*   **Uso:** Execute isso uma vez no início de um novo projeto.
*   **Descrição da Variante MCP:** `Configura a estrutura básica de arquivos e a configuração do Taskmaster no diretório atual para um novo projeto executando o comando 'task-master init'.`
*   **Principais Parâmetros/Opções MCP:**
    *   `projectName`: `Define o nome do seu projeto.` (CLI: `--name <nome>`)
    *   `projectDescription`: `Fornece uma breve descrição para o seu projeto.` (CLI: `--description <texto>`)
    *   `projectVersion`: `Define a versão inicial do seu projeto, por exemplo, '0.1.0'.` (CLI: `--version <versão>`)
    *   `authorName`: `Nome do autor.` (CLI: `--author <autor>`)
    *   `skipInstall`: `Ignora a instalação de dependências. O padrão é false.` (CLI: `--skip-install`)
    *   `addAliases`: `Adiciona aliases de shell tm e taskmaster. O padrão é false.` (CLI: `--aliases`)
    *   `yes`: `Ignora prompts e usa padrões/argumentos fornecidos. O padrão é false.` (CLI: `-y, --yes`)
*   **Uso:** Execute isso uma vez no início de um novo projeto, tipicamente via uma ferramenta integrada como o Cursor. Opera no diretório de trabalho atual do servidor MCP.
*   **Importante:** Uma vez concluído, você *DEVE* analisar um PRD para gerar tarefas. Não haverá arquivos de tarefas até então. O próximo passo após a inicialização deve ser criar um PRD usando o exemplo de PRD em .taskmaster/templates/example_prd.txt.

### 2. Analisar PRD (`parse_prd`)

*   **Ferramenta MCP:** `parse_prd`
*   **Comando CLI:** `task-master parse-prd [arquivo] [opções]`
*   **Descrição:** `Analisa um Documento de Requisitos de Produto, PRD, ou arquivo de texto com o Taskmaster para gerar automaticamente um conjunto inicial de tarefas em tasks.json.`
*   **Principais Parâmetros/Opções:**
    *   `input`: `Caminho para o seu PRD ou arquivo de texto de requisitos que o Taskmaster deve analisar para tarefas.` (CLI: `[arquivo]` posicional ou `-i, --input <arquivo>`)
    *   `output`: `Especifica onde o Taskmaster deve salvar o arquivo 'tasks.json' gerado. O padrão é '.taskmaster/tasks/tasks.json'.` (CLI: `-o, --output <arquivo>`)
    *   `numTasks`: `Número aproximado de tarefas de nível superior que o Taskmaster deve tentar gerar a partir do documento.` (CLI: `-n, --num-tasks <número>`)
    *   `force`: `Use isso para permitir que o Taskmaster sobrescreva um 'tasks.json' existente sem pedir confirmação.` (CLI: `-f, --force`)
*   **Uso:** Útil para iniciar um projeto a partir de um documento de requisitos existente.
*   **Notas:** O Task Master aderirá estritamente a quaisquer requisitos específicos mencionados no PRD, como bibliotecas, schemas de banco de dados, frameworks, pilhas de tecnologia, etc., preenchendo quaisquer lacunas onde o PRD não estiver totalmente especificado. As tarefas são projetadas para fornecer o caminho de implementação mais direto, evitando o excesso de engenharia.
*   **Importante:** Esta ferramenta MCP faz chamadas de IA e pode levar até um minuto para ser concluída. Por favor, informe os usuários para aguardarem enquanto a operação está em andamento. Se o usuário não tiver um PRD, sugira discutir sua ideia e, em seguida, use o exemplo de PRD em `.taskmaster/templates/example_prd.txt` como um modelo para criar o PRD com base em sua ideia, para uso com `parse-prd`.

---

## Configuração do Modelo de IA

### 2. Gerenciar Modelos (`models`)
*   **Ferramenta MCP:** `models`
*   **Comando CLI:** `task-master models [opções]`
*   **Descrição:** `Visualiza a configuração atual do modelo de IA ou define modelos específicos para diferentes funções (principal, pesquisa, fallback). Permite definir IDs de modelo personalizados para Ollama e OpenRouter.`
*   **Principais Parâmetros/Opções MCP:**
    *   `setMain <model_id>`: `Define o ID do modelo principal para geração/atualização de tarefas.` (CLI: `--set-main <model_id>`)
    *   `setResearch <model_id>`: `Define o ID do modelo para operações baseadas em pesquisa.` (CLI: `--set-research <model_id>`)
    *   `setFallback <model_id>`: `Define o ID do modelo a ser usado se o principal falhar.` (CLI: `--set-fallback <model_id>`)
    *   `ollama <boolean>`: `Indica que o ID do modelo definido é um modelo Ollama personalizado.` (CLI: `--ollama`)
    *   `openrouter <boolean>`: `Indica que o ID do modelo definido é um modelo OpenRouter personalizado.` (CLI: `--openrouter`)
    *   `listAvailableModels <boolean>`: `Se true, lista os modelos disponíveis que não estão atualmente atribuídos a uma função.` (CLI: Sem equivalente direto; CLI lista os disponíveis automaticamente)
    *   `projectRoot <string>`: `Opcional. Caminho absoluto para o diretório raiz do projeto.` (CLI: Determinado automaticamente)
*   **Principais Opções CLI:**
    *   `--set-main <model_id>`: `Define o modelo principal.`
    *   `--set-research <model_id>`: `Define o modelo de pesquisa.`
    *   `--set-fallback <model_id>`: `Define o modelo de fallback.`
    *   `--ollama`: `Especifica que o ID do modelo fornecido é para Ollama (use com --set-*).`
    *   `--openrouter`: `Especifica que o ID do modelo fornecido é para OpenRouter (use com --set-*). Valida contra a API do OpenRouter.`
    *   `--setup`: `Executa a configuração interativa para configurar modelos, incluindo IDs personalizados de Ollama/OpenRouter.`
*   **Uso (MCP):** Chame sem flags de conjunto para obter a configuração atual. Use `setMain`, `setResearch` ou `setFallback` com um ID de modelo válido para atualizar a configuração. Use `listAvailableModels: true` para obter uma lista de modelos não atribuídos. Para definir um modelo personalizado, forneça o ID do modelo e defina `ollama: true` ou `openrouter: true`.
*   **Uso (CLI):** Execute sem flags para visualizar a configuração atual e os modelos disponíveis. Use flags de conjunto para atualizar funções específicas. Use `--setup` para configuração guiada, incluindo modelos personalizados. Para definir um modelo personalizado via flags, use `--set-<função>=<model_id>` junto com `--ollama` ou `--openrouter`.
*   **Notas:** A configuração é armazenada em `.taskmaster/config.json` na raiz do projeto. Este comando/ferramenta modifica esse arquivo. Use `listAvailableModels` ou `task-master models` para ver os modelos suportados internamente. Os modelos personalizados do OpenRouter são validados contra sua API ao vivo. Os modelos personalizados do Ollama não são validados ao vivo.
*   **Nota da API:** As chaves de API para os provedores de IA selecionados (com base em seu modelo) precisam existir no arquivo mcp.json para serem acessíveis no contexto MCP. As chaves de API devem estar presentes no arquivo .env local para que a CLI possa lê-las.
*   **Custos do modelo:** Os custos nos modelos suportados são expressos em dólares. Um valor de entrada/saída de 3 é $3,00. Um valor de 0,8 é $0,80.
*   **Aviso:** NÃO EDITE MANUALMENTE O ARQUIVO .taskmaster/config.json. Use os comandos incluídos no formato MCP ou CLI conforme necessário. Sempre priorize as ferramentas MCP quando disponíveis e use a CLI como fallback.

---

## Listagem e Visualização de Tarefas

### 3. Obter Tarefas (`get_tasks`)

*   **Ferramenta MCP:** `get_tasks`
*   **Comando CLI:** `task-master list [opções]`
*   **Descrição:** `Lista suas tarefas do Taskmaster, opcionalmente filtrando por status e mostrando subtarefas.`
*   **Principais Parâmetros/Opções:**
    *   `status`: `Mostra apenas as tarefas do Taskmaster que correspondem a este status, por exemplo, 'pending' ou 'done'.` (CLI: `-s, --status <status>`)
    *   `withSubtasks`: `Inclui subtarefas recuadas sob suas tarefas pai na lista.` (CLI: `--with-subtasks`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Obtenha uma visão geral do status do projeto, frequentemente usado no início de uma sessão de trabalho.

### 4. Obter Próxima Tarefa (`next_task`)

*   **Ferramenta MCP:** `next_task`
*   **Comando CLI:** `task-master next [opções]`
*   **Descrição:** `Pede ao Taskmaster para mostrar a próxima tarefa disponível em que você pode trabalhar, com base no status e nas dependências concluídas.`
*   **Principais Parâmetros/Opções:**
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Identifique o que trabalhar em seguida de acordo com o plano.

### 5. Obter Detalhes da Tarefa (`get_task`)

*   **Ferramenta MCP:** `get_task`
*   **Comando CLI:** `task-master show [id] [opções]`
*   **Descrição:** `Exibe informações detalhadas para uma tarefa ou subtarefa específica do Taskmaster por seu ID.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `Obrigatório. O ID da tarefa do Taskmaster, por exemplo, '15', ou subtarefa, por exemplo, '15.2', que você deseja visualizar.` (CLI: `[id]` posicional ou `-i, --id <id>`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Entenda todos os detalhes, notas de implementação e estratégia de teste para uma tarefa específica antes de iniciar o trabalho.

---

## Criação e Modificação de Tarefas

### 6. Adicionar Tarefa (`add_task`)

*   **Ferramenta MCP:** `add_task`
*   **Comando CLI:** `task-master add-task [opções]`
*   **Descrição:** `Adiciona uma nova tarefa ao Taskmaster descrevendo-a; a IA a estruturará.`
*   **Principais Parâmetros/Opções:**
    *   `prompt`: `Obrigatório. Descreva a nova tarefa que você deseja que o Taskmaster crie, por exemplo, "Implementar autenticação de usuário usando JWT".` (CLI: `-p, --prompt <texto>`)
    *   `dependencies`: `Especifica os IDs de quaisquer tarefas do Taskmaster que devem ser concluídas antes que esta nova possa começar, por exemplo, '12,14'.` (CLI: `-d, --dependencies <ids>`)
    *   `priority`: `Define a prioridade para a nova tarefa: 'high', 'medium' ou 'low'. O padrão é 'medium'.` (CLI: `--priority <prioridade>`)
    *   `research`: `Permite que o Taskmaster use a função de pesquisa para uma criação de tarefa potencialmente mais informada.` (CLI: `-r, --research`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Adicione rapidamente tarefas recém-identificadas durante o desenvolvimento.
*   **Importante:** Esta ferramenta MCP faz chamadas de IA e pode levar até um minuto para ser concluída. Por favor, informe os usuários para aguardarem enquanto a operação está em andamento.

### 7. Adicionar Subtarefa (`add_subtask`)

*   **Ferramenta MCP:** `add_subtask`
*   **Comando CLI:** `task-master add-subtask [opções]`
*   **Descrição:** `Adiciona uma nova subtarefa a uma tarefa pai do Taskmaster, ou converte uma tarefa existente em uma subtarefa.`
*   **Principais Parâmetros/Opções:**
    *   `id` / `parent`: `Obrigatório. O ID da tarefa do Taskmaster que será a pai.` (MCP: `id`, CLI: `-p, --parent <id>`)
    *   `taskId`: `Use isso se você deseja converter uma tarefa de nível superior existente do Taskmaster em uma subtarefa do pai especificado.` (CLI: `-i, --task-id <id>`)
    *   `title`: `Obrigatório se não estiver usando taskId. O título para a nova subtarefa que o Taskmaster deve criar.` (CLI: `-t, --title <título>`)
    *   `description`: `Uma breve descrição para a nova subtarefa.` (CLI: `-d, --description <texto>`)
    *   `details`: `Fornece notas de implementação ou detalhes para a nova subtarefa.` (CLI: `--details <texto>`)
    *   `dependencies`: `Especifica IDs de outras tarefas ou subtarefas, por exemplo, '15' ou '16.1', que devem ser feitas antes desta nova subtarefa.` (CLI: `--dependencies <ids>`)
    *   `status`: `Define o status inicial para a nova subtarefa. O padrão é 'pending'.` (CLI: `-s, --status <status>`)
    *   `skipGenerate`: `Impede que o Taskmaster regenere automaticamente os arquivos de tarefa markdown após adicionar a subtarefa.` (CLI: `--skip-generate`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Divida tarefas manualmente ou reorganize tarefas existentes.

### 8. Atualizar Tarefas (`update`)

*   **Ferramenta MCP:** `update`
*   **Comando CLI:** `task-master update [opções]`
*   **Descrição:** `Atualiza várias tarefas futuras no Taskmaster com base em novo contexto ou alterações, começando de um ID de tarefa específico.`
*   **Principais Parâmetros/Opções:**
    *   `from`: `Obrigatório. O ID da primeira tarefa que o Taskmaster deve atualizar. Todas as tarefas com este ID ou superior que não estão 'done' serão consideradas.` (CLI: `--from <id>`)
    *   `prompt`: `Obrigatório. Explica a alteração ou o novo contexto para o Taskmaster aplicar às tarefas, por exemplo, "Estamos agora usando React Query em vez de Redux Toolkit para busca de dados".` (CLI: `-p, --prompt <texto>`)
    *   `research`: `Permite que o Taskmaster use a função de pesquisa para atualizações mais informadas. Requer chave de API apropriada.` (CLI: `-r, --research`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Lida com alterações significativas de implementação ou pivôs que afetam várias tarefas futuras. Exemplo CLI: `task-master update --from='18' --prompt='Mudando para React Query.\nPrecisa refatorar a busca de dados...'`
*   **Importante:** Esta ferramenta MCP faz chamadas de IA e pode levar até um minuto para ser concluída. Por favor, informe os usuários para aguardarem enquanto a operação está em andamento.

### 9. Atualizar Tarefa (`update_task`)

*   **Ferramenta MCP:** `update_task`
*   **Comando CLI:** `task-master update-task [opções]`
*   **Descrição:** `Modifica uma tarefa ou subtarefa específica do Taskmaster por seu ID, incorporando novas informações ou alterações.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `Obrigatório. O ID específico da tarefa do Taskmaster, por exemplo, '15', ou subtarefa, por exemplo, '15.2', que você deseja atualizar.` (CLI: `-i, --id <id>`)
    *   `prompt`: `Obrigatório. Explica as alterações específicas ou fornece as novas informações que o Taskmaster deve incorporar a esta tarefa.` (CLI: `-p, --prompt <texto>`)
    *   `research`: `Permite que o Taskmaster use a função de pesquisa para atualizações mais informadas. Requer chave de API apropriada.` (CLI: `-r, --research`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Refina uma tarefa específica com base em nova compreensão ou feedback. Exemplo CLI: `task-master update-task --id='15' --prompt='Esclarecimento: Use PostgreSQL em vez de MySQL.\nAtualizar detalhes do schema...'`
*   **Importante:** Esta ferramenta MCP faz chamadas de IA e pode levar até um minuto para ser concluída. Por favor, informe os usuários para aguardarem enquanto a operação está em andamento.

### 10. Atualizar Subtarefa (`update_subtask`)

*   **Ferramenta MCP:** `update_subtask`
*   **Comando CLI:** `task-master update-subtask [opções]`
*   **Descrição:** `Anexa notas ou detalhes com carimbo de data/hora a uma subtarefa específica do Taskmaster sem sobrescrever o conteúdo existente. Destinado ao registro iterativo da implementação.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `Obrigatório. O ID específico da subtarefa do Taskmaster, por exemplo, '15.2', à qual você deseja adicionar informações.` (CLI: `-i, --id <id>`)
    *   `prompt`: `Obrigatório. Fornece as informações ou notas que o Taskmaster deve anexar aos detalhes da subtarefa. Garanta que isso adicione *novas* informações não presentes anteriormente.` (CLI: `-p, --prompt <texto>`)
    *   `research`: `Permite que o Taskmaster use a função de pesquisa para atualizações mais informadas. Requer chave de API apropriada.` (CLI: `-r, --research`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Adicione notas de implementação, trechos de código ou esclarecimentos a uma subtarefa durante o desenvolvimento. Antes de chamar, revise os detalhes atuais da subtarefa para anexar apenas novos insights, ajudando a construir um log detalhado da jornada de implementação e evitar redundância. Exemplo CLI: `task-master update-subtask --id='15.2' --prompt='Descobri que a API requer o cabeçalho X.\nA implementação precisa de ajuste...'`
*   **Importante:** Esta ferramenta MCP faz chamadas de IA e pode levar até um minuto para ser concluída. Por favor, informe os usuários para aguardarem enquanto a operação está em andamento.

### 11. Definir Status da Tarefa (`set_task_status`)

*   **Ferramenta MCP:** `set_task_status`
*   **Comando CLI:** `task-master set-status [opções]`
*   **Descrição:** `Atualiza o status de uma ou mais tarefas ou subtarefas do Taskmaster, por exemplo, 'pending', 'in-progress', 'done'.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `Obrigatório. O(s) ID(s) da(s) tarefa(s) ou subtarefa(s) do Taskmaster, por exemplo, '15', '15.2' ou '16,17.1', a serem atualizadas.` (CLI: `-i, --id <id>`)
    *   `status`: `Obrigatório. O novo status a ser definido, por exemplo, 'done', 'pending', 'in-progress', 'review', 'cancelled'.` (CLI: `-s, --status <status>`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Marque o progresso à medida que as tarefas avançam no ciclo de desenvolvimento.

### 12. Remover Tarefa (`remove_task`)

*   **Ferramenta MCP:** `remove_task`
*   **Comando CLI:** `task-master remove-task [opções]`
*   **Descrição:** `Remove permanentemente uma tarefa ou subtarefa da lista de tarefas do Taskmaster.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `Obrigatório. O ID da tarefa do Taskmaster, por exemplo, '5', ou subtarefa, por exemplo, '5.2', a ser removida permanentemente.` (CLI: `-i, --id <id>`)
    *   `yes`: `Ignora o prompt de confirmação e exclui imediatamente a tarefa.` (CLI: `-y, --yes`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Exclua permanentemente tarefas ou subtarefas que não são mais necessárias no projeto.
*   **Notas:** Use com cautela, pois esta operação não pode ser desfeita. Considere usar o status 'blocked', 'cancelled' ou 'deferred' se você apenas deseja excluir uma tarefa do planejamento ativo, mas mantê-la para referência. O comando limpa automaticamente as referências de dependência em outras tarefas.

---

## Estrutura e Detalhamento de Tarefas

### 13. Expandir Tarefa (`expand_task`)

*   **Ferramenta MCP:** `expand_task`
*   **Comando CLI:** `task-master expand [opções]`
*   **Descrição:** `Usa a IA do Taskmaster para detalhar uma tarefa complexa em subtarefas menores e gerenciáveis. Anexa subtarefas por padrão.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `O ID da tarefa específica do Taskmaster que você deseja detalhar em subtarefas.` (CLI: `-i, --id <id>`)
    *   `num`: `Opcional: Sugere quantas subtarefas o Taskmaster deve tentar criar. Usa análise de complexidade/padrões caso contrário.` (CLI: `-n, --num <número>`)
    *   `research`: `Permite que o Taskmaster use a função de pesquisa para uma geração de subtarefas mais informada. Requer chave de API apropriada.` (CLI: `-r, --research`)
    *   `prompt`: `Opcional: Fornece contexto extra ou instruções específicas para o Taskmaster gerar as subtarefas.` (CLI: `-p, --prompt <texto>`)
    *   `force`: `Opcional: Se true, limpa as subtarefas existentes antes de gerar novas. O padrão é false (anexar).` (CLI: `--force`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Gere um plano de implementação detalhado para uma tarefa complexa antes de iniciar a codificação. Usa automaticamente as recomendações do relatório de complexidade se disponível e `num` não for especificado.
*   **Importante:** Esta ferramenta MCP faz chamadas de IA e pode levar até um minuto para ser concluída. Por favor, informe os usuários para aguardarem enquanto a operação está em andamento.

### 14. Expandir Todas as Tarefas (`expand_all`)

*   **Ferramenta MCP:** `expand_all`
*   **Comando CLI:** `task-master expand --all [opções]` (Nota: CLI usa o comando `expand` com a flag `--all`)
*   **Descrição:** `Instrui o Taskmaster a expandir automaticamente todas as tarefas pendentes/em andamento elegíveis com base na análise de complexidade ou padrões. Anexa subtarefas por padrão.`
*   **Principais Parâmetros/Opções:**
    *   `num`: `Opcional: Sugere quantas subtarefas o Taskmaster deve tentar criar por tarefa.` (CLI: `-n, --num <número>`)
    *   `research`: `Permite a função de pesquisa para uma geração de subtarefas mais informada. Requer chave de API apropriada.` (CLI: `-r, --research`)
    *   `prompt`: `Opcional: Fornece contexto extra para o Taskmaster aplicar geralmente durante a expansão.` (CLI: `-p, --prompt <texto>`)
    *   `force`: `Opcional: Se true, limpa as subtarefas existentes antes de gerar novas para cada tarefa elegível. O padrão é false (anexar).` (CLI: `--force`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Útil após a geração inicial de tarefas ou análise de complexidade para detalhar várias tarefas de uma vez.
*   **Importante:** Esta ferramenta MCP faz chamadas de IA e pode levar até um minuto para ser concluída. Por favor, informe os usuários para aguardarem enquanto a operação está em andamento.

### 15. Limpar Subtarefas (`clear_subtasks`)

*   **Ferramenta MCP:** `clear_subtasks`
*   **Comando CLI:** `task-master clear-subtasks [opções]`
*   **Descrição:** `Remove todas as subtarefas de uma ou mais tarefas pai do Taskmaster especificadas.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `O(s) ID(s) da(s) tarefa(s) pai do Taskmaster cujas subtarefas você deseja remover, por exemplo, '15' ou '16,18'. Obrigatório, a menos que use `all`.) (CLI: `-i, --id <ids>`)
    *   `all`: `Instrui o Taskmaster a remover subtarefas de todas as tarefas pai.` (CLI: `--all`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Usado antes de regenerar subtarefas com `expand_task` se o detalhamento anterior precisar ser substituído.

### 16. Remover Subtarefa (`remove_subtask`)

*   **Ferramenta MCP:** `remove_subtask`
*   **Comando CLI:** `task-master remove-subtask [opções]`
*   **Descrição:** `Remove uma subtarefa de seu pai do Taskmaster, opcionalmente convertendo-a em uma tarefa autônoma.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `Obrigatório. O(s) ID(s) da(s) subtarefa(s) do Taskmaster a serem removidas, por exemplo, '15.2' ou '16.1,16.3'.` (CLI: `-i, --id <id>`)
    *   `convert`: `Se usado, o Taskmaster transformará a subtarefa em uma tarefa de nível superior regular em vez de excluí-la.` (CLI: `-c, --convert`)
    *   `skipGenerate`: `Impede que o Taskmaster regenere automaticamente os arquivos de tarefa markdown após remover a subtarefa.` (CLI: `--skip-generate`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Exclua subtarefas desnecessárias ou promova uma subtarefa a uma tarefa de nível superior.

### 17. Mover Tarefa (`move_task`)

*   **Ferramenta MCP:** `move_task`
*   **Comando CLI:** `task-master move [opções]`
*   **Descrição:** `Move uma tarefa ou subtarefa para uma nova posição na hierarquia de tarefas.`
*   **Principais Parâmetros/Opções:**
    *   `from`: `Obrigatório. ID da tarefa/subtarefa a ser movida (por exemplo, "5" ou "5.2"). Pode ser separado por vírgulas para várias tarefas.` (CLI: `--from <id>`)
    *   `to`: `Obrigatório. ID do destino (por exemplo, "7" ou "7.3"). Deve corresponder ao número de IDs de origem se separado por vírgulas.` (CLI: `--to <id>`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Reorganize tarefas movendo-as dentro da hierarquia. Suporta vários casos de uso como:
    *   Mover uma tarefa autônoma para se tornar uma subtarefa (por exemplo, `--from=5 --to=7`)
    *   Mover uma subtarefa para se tornar uma tarefa autônoma (por exemplo, `--from=5.2 --to=7`)
    *   Mover uma subtarefa para um pai diferente (por exemplo, `--from=5.2 --to=7.3`)
    *   Reordenar subtarefas dentro do mesmo pai (por exemplo, `--from=5.2 --to=5.4`)
    *   Mover uma tarefa para uma nova posição de ID não existente (por exemplo, `--from=5 --to=25`)
    *   Mover várias tarefas de uma vez usando IDs separados por vírgulas (por exemplo, `--from=10,11,12 --to=16,17,18`)
*   **Recursos de Validação:**
    *   Permite mover tarefas para IDs de destino não existentes (cria tarefas de espaço reservado)
    *   Impede o movimento para IDs de tarefas existentes que já possuem conteúdo (para evitar sobrescrever)
    *   Valida se as tarefas de origem existem antes de tentar movê-las
    *   Mantém relacionamentos pai-filho adequados
*   **Exemplo CLI:** `task-master move --from=5.2 --to=7.3` para mover a subtarefa 5.2 para se tornar a subtarefa 7.3.
*   **Exemplo de Múltiplos Movimentos:** `task-master move --from=10,11,12 --to=16,17,18` para mover várias tarefas para novas posições.
*   **Uso Comum:** Resolvendo conflitos de mesclagem em tasks.json quando vários membros da equipe criam tarefas em branches diferentes.

---

## Gerenciamento de Dependências

### 18. Adicionar Dependência (`add_dependency`)

*   **Ferramenta MCP:** `add_dependency`
*   **Comando CLI:** `task-master add-dependency [opções]`
*   **Descrição:** `Define uma dependência no Taskmaster, tornando uma tarefa um pré-requisito para outra.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `Obrigatório. O ID da tarefa do Taskmaster que dependerá de outra.` (CLI: `-i, --id <id>`)
    *   `dependsOn`: `Obrigatório. O ID da tarefa do Taskmaster que deve ser concluída primeiro, o pré-requisito.` (CLI: `-d, --depends-on <id>`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <caminho>`)
*   **Uso:** Estabeleça a ordem correta de execução entre as tarefas.

### 19. Remover Dependência (`remove_dependency`)

*   **Ferramenta MCP:** `remove_dependency`
*   **Comando CLI:** `task-master remove-dependency [opções]`
*   **Descrição:** `Remove um relacionamento de dependência entre duas tarefas do Taskmaster.`
*   **Principais Parâmetros/Opções:**
    *   `id`: `Obrigatório. O ID da tarefa do Taskmaster da qual você deseja remover um pré-requisito.` (CLI: `-i, --id <id>`)
    *   `dependsOn`: `Obrigatório. O ID da tarefa do Taskmaster que não deve mais ser um pré-requisito.` (CLI: `-d, --depends-on <id>`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Atualize os relacionamentos de tarefas quando a ordem de execução mudar.

### 20. Validar Dependências (`validate_dependencies`)

*   **Ferramenta MCP:** `validate_dependencies`
*   **Comando CLI:** `task-master validate-dependencies [opções]`
*   **Descrição:** `Verifica suas tarefas do Taskmaster em busca de problemas de dependência (como referências circulares ou links para tarefas não existentes) sem fazer alterações.`
*   **Principais Parâmetros/Opções:**
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Audite a integridade de suas dependências de tarefas.

### 21. Corrigir Dependências (`fix_dependencies`)

*   **Ferramenta MCP:** `fix_dependencies`
*   **Comando CLI:** `task-master fix-dependencies [opções]`
*   **Descrição:** `Corrige automaticamente problemas de dependência (como referências circulares ou links para tarefas não existentes) em suas tarefas do Taskmaster.`
*   **Principais Parâmetros/Opções:**
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Limpe os erros de dependência automaticamente.

---

## Análise e Relatórios

### 22. Analisar Complexidade do Projeto (`analyze_project_complexity`)

*   **Ferramenta MCP:** `analyze_project_complexity`
*   **Comando CLI:** `task-master analyze-complexity [opções]`
*   **Descrição:** `Pede ao Taskmaster para analisar suas tarefas para determinar sua complexidade e sugerir quais precisam ser detalhadas ainda mais.`
*   **Principais Parâmetros/Opções:**
    *   `output`: `Onde salvar o relatório de análise de complexidade (padrão: '.taskmaster/reports/task-complexity-report.json').` (CLI: `-o, --output <arquivo>`)
    *   `threshold`: `A pontuação mínima de complexidade (1-10) que deve acionar uma recomendação para expandir uma tarefa.` (CLI: `-t, --threshold <número>`)
    *   `research`: `Permite a função de pesquisa para uma análise de complexidade mais precisa. Requer chave de API apropriada.` (CLI: `-r, --research`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Usado antes de detalhar tarefas para identificar quais precisam de mais atenção.
*   **Importante:** Esta ferramenta MCP faz chamadas de IA e pode levar até um minuto para ser concluída. Por favor, informe os usuários para aguardarem enquanto a operação está em andamento.

### 23. Visualizar Relatório de Complexidade (`complexity_report`)

*   **Ferramenta MCP:** `complexity_report`
*   **Comando CLI:** `task-master complexity-report [opções]`
*   **Descrição:** `Exibe o relatório de análise de complexidade da tarefa em um formato legível.`
*   **Principais Parâmetros/Opções:**
    *   `file`: `Caminho para o relatório de complexidade (padrão: '.taskmaster/reports/task-complexity-report.json').` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Revise e entenda os resultados da análise de complexidade após executar analyze-complexity.

---

## Gerenciamento de Arquivos

### 24. Gerar Arquivos de Tarefa (`generate`)

*   **Ferramenta MCP:** `generate`
*   **Comando CLI:** `task-master generate [opções]`
*   **Descrição:** `Cria ou atualiza arquivos Markdown individuais para cada tarefa com base no seu tasks.json.`
*   **Principais Parâmetros/Opções:**
    *   `output`: `O diretório onde o Taskmaster deve salvar os arquivos de tarefa (padrão: em um diretório 'tasks').` (CLI: `-o, --output <diretório>`)
    *   `file`: `Caminho para o seu arquivo 'tasks.json' do Taskmaster. O padrão depende da detecção automática.` (CLI: `-f, --file <arquivo>`)
*   **Uso:** Execute isso depois de fazer alterações em tasks.json para manter os arquivos de tarefa individuais atualizados.

---

## Configuração de Variáveis de Ambiente (Atualizado)

O Taskmaster usa principalmente o arquivo **`.taskmaster/config.json`** (na raiz do projeto) para configuração (modelos, parâmetros, nível de log, etc.), gerenciado via `task-master models --setup`.

As variáveis de ambiente são usadas **apenas** para chaves de API sensíveis relacionadas a provedores de IA e substituições específicas como a URL base do Ollama:

*   **Chaves de API (Obrigatório para o provedor correspondente):**
    *   `ANTHROPIC_API_KEY`
    *   `PERPLEXITY_API_KEY`
    *   `OPENAI_API_KEY`
    *   `GOOGLE_API_KEY`
    *   `MISTRAL_API_KEY`
    *   `AZURE_OPENAI_API_KEY` (Requer `AZURE_OPENAI_ENDPOINT` também)
    *   `OPENROUTER_API_KEY`
    *   `XAI_API_KEY`
    *   `OLLANA_API_KEY` (Requer `OLLAMA_BASE_URL` também)
*   **Endpoints (Opcional/Específico do Provedor dentro de .taskmaster/config.json):**
    *   `AZURE_OPENAI_ENDPOINT`
    *   `OLLAMA_BASE_URL` (Padrão: `http://localhost:11434/api`)

**Defina as chaves de API** em seu arquivo **`.env`** na raiz do projeto (para uso CLI) ou na seção `env` do seu arquivo **`.cursor/mcp.json`** (para integração MCP/Cursor). Todas as outras configurações (escolha do modelo, tokens máximos, temperatura, nível de log, endpoints personalizados) são gerenciadas em `.taskmaster/config.json` via comando `task-master models` ou ferramenta MCP `models`.

---

Para detalhes sobre como esses comandos se encaixam no processo de desenvolvimento, consulte o [Guia de Fluxo de Trabalho de Desenvolvimento](mdc:.cursor/rules/dev_workflow.mdc).<environment_details>
# VSCode Visible Files
.clinerules/tooling/cursor-rules.md

# VSCode Open Tabs
harmoniza-facil-agendas/.next/types/app/layout.ts
harmoniza-facil-agendas/.next/types/app/page.ts
harmoniza-facil-agendas/.next/types/app/paciente/page.ts
harmoniza-facil-agendas/.next/types/app/admin/page.ts
neonpro/tailwind.config.ts
neonpro/src/index.css
neonpro/src/components/ThemeToggle.tsx
neonpro/src/pages/AuthPage.tsx
neonpro/src/contexts/auth/useAuthOperations.ts
memory-bank/global-standards.md
memory-bank/global-learnings.md
neonpro/memory-bank/project-snapshot.md
neonpro/src/pages/Dashboard.tsx
neonpro/supabase/migrations/004_create_patient_medical_history.sql
neonpro/src/types/patient.ts
neonpro/src/hooks/usePatients.ts
neonpro/src/components/patients/PatientForm.tsx
neonpro/src/components/patients/PatientList.tsx
neonpro/src/pages/Clientes.tsx
neonpro/supabase/migrations/002_create_appointments.sql
neonpro/src/types/appointment.ts
neonpro/src/hooks/useAppointments.ts
neonpro/src/components/appointments/AppointmentForm.tsx
neonpro/src/components/appointments/AppointmentList.tsx
neonpro/src/pages/Agendamentos.tsx
neonpro/src/App.tsx
.windsurfrules
neonpro/src/types/transaction.ts
neonpro/src/hooks/useTransactions.ts
neonpro/src/components/transactions/TransactionForm.tsx
neonpro/src/components/transactions/TransactionList.tsx
neonpro/src/pages/Financeiro.tsx
neonpro/src/pages/Relatorios.tsx
neonpro/src/components/AppRouter.tsx
neonpro/src/components/Layout.tsx
neonpro/supabase/migrations/005_create_user_profiles.sql
neonpro/src/types/user.ts
neonpro/src/hooks/useUsers.ts
neonpro/src/components/users/UserForm.tsx
neonpro/src/components/users/UserList.tsx
neonpro/src/pages/Usuarios.tsx
neonpro/memory-bank/task-log.md
neonpro/memory-bank/learnings.md
.clinerules/master_rule.md
.clinerules/unified-protocol.md
.clinerules/completude-verification-protocol.md
.clinerules/sequential-thinking-mcp.md
.clinerules/workflows/coding_principles.md
.clinerules/workflows/error_handling_protocol.md
.clinerules/workflows/error_handling_protocol_v2.md
.env
TASK-MASTER-INTEGRATION-COMPLETE.md
VSCODE.code-workspace
test-git-setup.ps1
sync-existing-only.ps1
README-GITHUB-SETUP.md
quick-push.ps1
push-all-projects.ps1
memory-bank/workspace-task-log.md
memory-bank/global-project-overview.md
INSTRUCOES-FINAIS.md
execute-push-now.ps1
connect-existing-repos.ps1
auto-sync.ps1
auto-push.ps1
.clinerules/00-tooling-preferences.md
.clinerules/tooling/cursor-rules.md

# Current Time
6/3/2025, 10:31:11 AM (America/Sao_Paulo, UTC-3:00)

# Context Window Usage
149,999 / 1,048.576K tokens used (14%)

# Current Mode
ACT MODE
</environment_details>
