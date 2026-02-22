# 🧠 Memory Bank Index

Este é o mapa central de conhecimento do projeto. Agentes devem consultar este arquivo antes de qualquer tarefa para entender os padrões, decisões e o estado atual do sistema.

## 🗺️ Knowledge Items (KIs) Estruturais

- [architecture.md](file:///home/ils15/copilot-agents/docs/memory-bank/architecture.md): Visão geral da arquitetura de agentes e padrões técnicos.
- [standards.md](file:///home/ils15/copilot-agents/docs/memory-bank/standards.md): Padrões de código, testes e documentação. (TBD)
- [active-context.md](file:///home/ils15/copilot-agents/docs/memory-bank/active-context.md): O que estamos trabalhando agora e decisões recentes. (TBD)

## 📏 Padrões e Exemplos
- [Instruções de Uso](file:///home/ils15/copilot-agents/instructions/memory-bank-standards.instructions.md): Como usar, manter e migrar o Memory Bank.

## 📝 Exemplos de Chamadas de Agentes
- **Início de Projeto:** `@athena Analise o repo e inicialize o Memory Bank conforme os padrões.`
- **Pós-Implementação:** `@mnemosyne Documente o fluxo de login no Memory Bank.`
- **Consulta:** `@apollo Pesquise no Memory Bank como o banco de dados está configurado.`

## 🛠️ Como usar este Banco de Memória

1. **Leitura Obrigatória:** Antes de qualquer `athena:plan` ou `zeus:implement`, o agente deve ler este `index.md`.
2. **Atualização Orgânica:** Ao final de cada tarefa bem-sucedida, o agente responsável (geralmente Mnemosyne) deve atualizar os KIs relevantes.
3. **Redução de Ruído:** Evite criar novos arquivos `.md` fora deste diretório para documentação persistente.
