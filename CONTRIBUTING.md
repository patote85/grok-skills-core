# Contribuindo para o grok-skills-core

Obrigado por considerar contribuir com este repositório!

Este projeto contém skills do Grok focadas em agentes de IA de alta criticidade (sistemas Core financeiros). As contribuições são bem-vindas, mas precisam seguir um processo controlado para manter a qualidade e o rigor das skills.

## Como contribuir

### 1. Abra uma Issue primeiro
Antes de começar a trabalhar, abra uma **Issue** descrevendo:
- O que você quer adicionar ou melhorar
- Por que isso é útil
- Qual skill (ou ambas) será impactada

Isso evita trabalho duplicado e permite alinhamento prévio.

### 2. Faça um Fork do repositório
Clique em **Fork** no canto superior direito da página do repositório.

### 3. Crie uma branch a partir da `main`
```bash
git clone https://github.com/SEU-USUARIO/grok-skills-core.git
cd grok-skills-core
git checkout -b feature/nome-da-sua-contribuicao
```

### 4. Faça suas alterações
- Respeite a arquitetura de **Progressive Disclosure** (mantenha os `SKILL.md` leves).
- Qualquer alteração em restrições de Core (`core-constraints.md`) deve ser extremamente bem justificada.
- Siga o estilo de escrita já existente (direto, técnico e sem fluff).
- Se adicionar exemplos de código, mantenha o padrão: código em en-US + comentários em pt-BR.

### 5. Abra um Pull Request
- Envie o PR para a branch `main` do repositório original.
- Preencha o template de PR (se houver) ou descreva claramente o que foi alterado e por quê.
- Referencie a Issue correspondente (ex: `Closes #12`).

### 6. Code Review obrigatório
- **Nenhum merge na `main` ocorre sem code review do mantenedor** (`@patote85`).
- Responda aos comentários do review e faça os ajustes necessários.
- Após aprovação, o mantenedor fará o merge.

## O que NÃO é bem-vindo
- Alterações que enfraquecem as restrições de produção (idempotência, circuit breakers, audit trail, least privilege etc.).
- Adicionar complexidade desnecessária ou abstrações especulativas.
- PRs grandes demais sem discussão prévia na Issue.

## Dúvidas?
Abra uma Issue com a tag `question` ou mencione `@patote85`.

Obrigado por ajudar a manter este repositório rigoroso e útil!
