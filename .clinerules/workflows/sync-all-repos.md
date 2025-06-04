---
description: Workflow para sincronizar múltiplos repositórios Git no workspace.
globs: ["**/*"]
alwaysApply: true
tags: ["git", "workflow", "script", "automation", "sync"]
---

# Workflow de Sincronização de Múltiplos Repositórios Git

## 1. Objetivo

Este workflow automatiza o processo de sincronização de múltiplos repositórios Git dentro do workspace, garantindo que as alterações locais sejam preservadas, as atualizações remotas sejam incorporadas e tudo seja enviado de volta para os respectivos repositórios.

## 2. Script `sync-all-repos.ps1`

### 2.1. Funcionalidade
O script `sync-all-repos.ps1` executa as seguintes etapas para cada repositório especificado:
1. **Verifica o status do Git** e salva quaisquer alterações locais não commitadas usando `git stash`.
2. **Faz `git pull`** para buscar e mesclar as alterações do repositório remoto (assumindo a branch `main`).
3. **Resolve conflitos de merge** automaticamente se possível, ou indica a necessidade de resolução manual.
4. **Aplica as alterações salvas no stash** de volta ao diretório de trabalho.
5. **Adiciona e commita** todas as alterações locais restantes.
6. **Faz `git push`** para enviar todas as alterações para o repositório remoto.

O script também verifica se o diretório raiz do workspace é um repositório Git e o sincroniza, se aplicável.

### 2.2. Localização
O script está localizado na raiz do projeto: `sync-all-repos.ps1`.

### 2.3. Como Usar

#### Sintaxe Básica (PowerShell):
```powershell
./sync-all-repos.ps1
```
Este comando executará o script usando a mensagem de commit padrão: "Sincronização automática de repositórios".

#### Com Mensagem de Commit Personalizada:
```powershell
./sync-all-repos.ps1 -CommitMessage "Sincronização diária do workspace"
```
Substitua `"Sincronização diária do workspace"` pela sua mensagem desejada.

### 2.4. Conteúdo do Script (`sync-all-repos.ps1`)
```powershell
param (
    [string]$CommitMessage = "Sincronização automática de repositórios"
)

function Sync-GitRepository {
    param (
        [string]$RepoPath,
        [string]$CommitMessage
    )

    Write-Host "Iniciando sincronização para o repositório: $RepoPath" -ForegroundColor Cyan

    try {
        # Salvar o diretório atual e navegar para o repositório
        Push-Location -Path $RepoPath

        # 1. Verificar status e stashear alterações locais
        Write-Host "Verificando status do Git..."
        $status = git status
        Write-Host $status

        if ($status -match "Changes not staged for commit" -or $status -match "Changes to be committed") {
            Write-Host "Salvando alterações locais com git stash..."
            git stash push -m "Local changes before pull (${RepoPath})"
            if ($LASTEXITCODE -ne 0) {
                Write-Warning "Falha ao stashear alterações locais em $RepoPath. Tentando continuar."
            }
        } else {
            Write-Host "Nenhuma alteração local para stashear."
        }

        # 2. Fazer pull das alterações remotas
        Write-Host "Fazendo pull das alterações remotas..."
        git pull origin main # Assumindo 'main' como branch principal
        if ($LASTEXITCODE -ne 0) {
            Write-Error "Falha ao executar git pull em $RepoPath. Pode haver conflitos."
            # Tentar resolver conflitos automaticamente se possível
            $mergeStatus = git status
            if ($mergeStatus -match "All conflicts fixed but you are still merging") {
                Write-Host "Conflitos resolvidos automaticamente. Commitando merge..."
                git commit -m "Merge remote-tracking branch 'origin/main' for $RepoPath"
                if ($LASTEXITCODE -ne 0) {
                    throw "Falha ao commitar merge automático em $RepoPath."
                }
            } elseif ($mergeStatus -match "You have unmerged paths") {
                Write-Error "Conflitos manuais detectados em $RepoPath. Por favor, resolva-os manualmente e execute o script novamente."
                return $false # Indica falha para o script principal
            }
        }

        # 3. Aplicar stash de volta
        Write-Host "Aplicando alterações locais do stash..."
        $stashList = git stash list
        if ($stashList -match "Local changes before pull \(${RepoPath}\)") {
            git stash pop
            if ($LASTEXITCODE -ne 0) {
                Write-Warning "Falha ao aplicar stash em $RepoPath. Pode haver conflitos ao aplicar o stash."
                # Se houver conflitos ao aplicar o stash, o usuário precisará resolver manualmente
                $stashApplyStatus = git status
                if ($stashApplyStatus -match "Unmerged paths") {
                    Write-Error "Conflitos ao aplicar stash em $RepoPath. Por favor, resolva-os manualmente e execute o script novamente."
                    return $false
                }
            }
        } else {
            Write-Host "Nenhum stash para aplicar para $RepoPath."
        }

        # 4. Adicionar e commitar todas as alterações locais
        Write-Host "Adicionando todas as alterações ao staging..."
        git add .
        if ($LASTEXITCODE -ne 0) {
            Write-Warning "Falha ao adicionar arquivos ao staging em $RepoPath. Tentando continuar."
        }

        Write-Host "Fazendo commit das alterações locais..."
        git commit -m "$CommitMessage (${RepoPath})"
        if ($LASTEXITCODE -ne 0) {
            Write-Warning "Nenhuma alteração para commitar ou falha no commit em $RepoPath. Tentando push de qualquer forma."
        }

        # 5. Fazer push para o repositório remoto
        Write-Host "Fazendo push para o repositório remoto..."
        git push
        if ($LASTEXITCODE -ne 0) {
            throw "Falha ao executar git push em $RepoPath."
        }

        Write-Host "Sincronização concluída com sucesso para $RepoPath." -ForegroundColor Green
        return $true
    }
    catch {
        Write-Error "Ocorreu um erro durante a sincronização de $RepoPath: $_"
        return $false
    }
    finally {
        # Voltar para o diretório original
        Pop-Location
    }
}

# Captura o diretório base do script no início
$scriptBaseDir = (Get-Location).Path

# Lista de diretórios de repositórios a serem sincronizados
# Certifique-se de que estes caminhos são relativos ao diretório onde o script será executado
$repositories = @(
    "harmoniza-facil-agendas",
    "aegiswallet",
    "taskmaster-integration"
    # Adicione outros repositórios aqui, se houver
)

# Sincronizar o repositório raiz (se for um repositório Git)
Write-Host "Verificando o diretório raiz do workspace..."
try {
    Push-Location -Path $scriptBaseDir # Salva o diretório atual e navega para o base
    if ((Test-Path ".git") -and (git rev-parse --is-inside-work-tree 2>$null)) {
        Write-Host "Diretório raiz é um repositório Git. Sincronizando..." -ForegroundColor Yellow
        Sync-GitRepository -RepoPath $scriptBaseDir -CommitMessage $CommitMessage
    } else {
        Write-Host "Diretório raiz não é um repositório Git ou não está inicializado." -ForegroundColor Yellow
    }
}
catch {
    Write-Error "Erro ao verificar o diretório raiz: $_"
}
finally {
    Pop-Location # Retorna ao diretório salvo por Push-Location
}

# Sincronizar os outros repositórios
foreach ($repo in $repositories) {
    $fullPath = Join-Path $scriptBaseDir $repo
    if (Test-Path $fullPath) {
        if ((Test-Path (Join-Path $fullPath ".git")) -and (git -C $fullPath rev-parse --is-inside-work-tree 2>$null)) {
            Sync-GitRepository -RepoPath $fullPath -CommitMessage $CommitMessage
        } else {
            Write-Warning "O diretório '$repo' não é um repositório Git válido. Ignorando."
        }
    } else {
        Write-Warning "O diretório '$repo' não foi encontrado. Ignorando."
    }
}

Write-Host "Processo de sincronização de todos os repositórios concluído." -ForegroundColor Green
