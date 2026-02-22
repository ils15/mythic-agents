# 🏛️ Architecture & Core Patterns

O sistema de agentes do `copilot-agents` segue o padrão **Conductor-Delegate (Zeus-Subagents)**, otimizado para o ambiente VSCode Copilot.

## 🤖 Hierarquia de Agentes

| Agente | Nível | Responsabilidade Principal |
| :--- | :--- | :--- |
| **Zeus** | Orquestrador | Coordinação de fluxo, chamadas de subagentes e pause points. |
| **Athena** | Planejador | Estratégia, pesquisa e geração do `implementation_plan.md`. |
| **Apollo** | Scout | Descoberta rápida de codebase e pesquisa externa (Search/Fetch). |
| **Executores** | Implementação | Hermes (Backend), Aphrodite (Frontend), Maat (DB), Ra (Infra). |
| **Qualidade** | Verificação | Temis (Reviewer). |
| **Memória** | Persistência | Mnemosyne (Gerenciador do Memory Bank). |

## 🔄 Fluxo de Trabalho Progressivo

1. **Planning:** Athena gera o plano baseado nas descobertas do Apollo.
2. **Pause Point (User Approval):** O usuário valida o plano.
3. **Execution:** Agentes implementam usando TDD (RED -> GREEN -> REFACTOR).
4. **Verification:** Temis revisa o código contra os padrões definidos.
5. **Memory Update:** Mnemosyne destila o conhecimento da tarefa neste Memory Bank.

## 📋 Padrões Técnicos

- **TDD Rigoroso:** Teste falhando primeiro, cobertura mínima de 80%.
- **Contexto Otimizado:** Uso de resumos em vez de dumps de código no chat.
- **Hierarquia de Pastas:** `agents/`, `instructions/`, `prompts/`, `skills/`.
