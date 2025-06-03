---
description: Base de conhecimento consolidada e curada derivada de reflexões e aprendizados
version: 1.0
created: 2025-06-03
tags: ["consolidated", "learning", "knowledge-base", "actionable"]
---

# Consolidated Learnings

Este arquivo contém conhecimento curado, sintetizado e acionável derivado do `raw_reflection_log.md`. Representa a "segunda camada" do sistema de knowledge bank, focando em insights de alto valor e padrões reutilizáveis.

## Objetivo

Manter uma base de conhecimento refinada, organizada e facilmente consultável que:
- Acelere futuras tarefas similares
- Evite repetição de erros conhecidos
- Forneça padrões e técnicas comprovadamente eficazes
- Sirva como referência rápida para decisões técnicas

## Organização

O conhecimento está organizado por categorias para facilitar a recuperação:

### 🛠️ Padrões Técnicos Gerais

*Padrões e técnicas reutilizáveis aplicáveis a múltiplos projetos*

### 📋 Gestão de Projetos e Workflows

*Metodologias, processos e práticas de gestão comprovadamente eficazes*

### 🔧 Ferramentas e Configurações

*Configurações específicas, comandos úteis e otimizações de ferramentas*

### 🐛 Resolução de Problemas

*Padrões de erro comuns e suas soluções documentadas*

### 🚀 Otimizações de Performance

*Técnicas e estratégias para melhorar eficiência e velocidade*

### 💡 Insights de UX/UI

*Padrões de interface e experiência do usuário que funcionam bem*

### 🔒 Segurança e Melhores Práticas

*Práticas de segurança e padrões de código seguro*

### 📝 Projetos Específicos

*Conhecimento específico por projeto (NeonPro, AegisWallet, HarmonizaFácil, etc.)*

## Guidelines para Manutenção

- **Alta Densidade de Valor**: Apenas insights acionáveis e reutilizáveis
- **Clareza e Concisão**: Linguagem direta e exemplos práticos
- **Organização Lógica**: Fácil navegação e busca
- **Atualização Contínua**: Remove informações obsoletas, adiciona novos padrões
- **Rastreabilidade**: Referencia origem quando relevante

## Métricas de Qualidade

- **Reutilização**: Quantas vezes um padrão foi aplicado com sucesso
- **Prevenção de Erros**: Quantos erros foram evitados por seguir um padrão
- **Economia de Tempo**: Redução de tempo em tarefas similares
- **Consistência**: Uniformidade na aplicação de padrões

---

## Base de Conhecimento Consolidada

### 🛠️ Padrões Técnicos Gerais

<!-- Padrões serão consolidados automaticamente do raw_reflection_log.md -->

### 📋 Gestão de Projetos e Workflows

**Pattern: Protocolo Unificado de 4 Camadas**
- **Descrição**: Sistema estruturado para garantir continuidade, melhoria e verificação
- **Aplicação**: Obrigatório em todas as tarefas complexas
- **Benefícios**: Reduz retrabalho, captura conhecimento, melhora qualidade
- **Rationale**: Garante que nenhuma tarefa seja finalizada sem verificação e aprendizado

### 🔧 Ferramentas e Configurações

**Pattern: Integração Taskmaster + Sequential Thinking**
- **Configuração**: `.clinerules/00-tooling-preferences.md` proíbe mcp-r-task-manager
- **Uso Taskmaster**: Para gerenciamento de tarefas via CLI (https://github.com/eyaltoledano/claude-task-master)
- **Uso Sequential Thinking**: Para análise complexa via MCP server
- **Benefícios**: Complementaridade entre gestão e análise profunda

### 🐛 Resolução de Problemas

**Pattern: Error Handling Protocol**
- **Ativação**: Primeira ocorrência de erro que impede conclusão de sub-tarefa
- **Processo**: Diagnóstico > Correção > Registro > Prevenção
- **Ferramentas**: Coordenação com sequential-thinking para análise complexa

### 📝 Projetos Específicos

#### NeonPro - Sistema de Gestão de Clínica
- **Stack**: React + TypeScript + Supabase + Tailwind CSS
- **Arquitetura**: Componentes modulares com hooks customizados
- **Padrões**: Hooks para entidades (usePatients, useAppointments, useTransactions)

#### AegisWallet - Carteira de Criptomoedas
- **Stack**: React + TypeScript + Vite + Supabase
- **Foco**: Segurança e user experience

#### HarmonizaFácil - Sistema de Agendamentos
- **Stack**: Next.js + TypeScript + Tailwind CSS
- **Especialização**: Agendamento otimizado

---

*Esta base de conhecimento é atualizada continuamente através do processo de consolidação definido no protocolo de melhoria contínua.*
