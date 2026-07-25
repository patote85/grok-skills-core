# grok-skills-core

Coleção versionada de **skills do Grok** projetadas para construir e operar agentes de IA que produzem código real de produção para sistemas Core financeiros de alta criticidade (tolerância zero a downtime).

Essas skills seguem uma arquitetura de **Progressive Disclosure** inspirada nas orientações mais recentes de context engineering da Anthropic para os modelos Claude 5: manter o ponto de entrada leve, carregar orientações detalhadas apenas quando necessário e nunca over-constrain o modelo com regras que os modelos mais novos já conseguem lidar com julgamento.

## Princípios de Design

- **Restrições hard de Core permanecem não-negociáveis** (idempotência, circuit breakers, trilhas de auditoria, least privilege, human-in-the-loop para ações de alto risco).
- Todo o resto usa progressive disclosure para evitar inchaço de contexto e instruções conflitantes.
- As skills são complementares e intencionalmente separadas:
  - Uma decide **arquitetura e prontidão de produção**.
  - A outra disciplina a **qualidade de implementação de código**.

## Skills

### 1. `ai-agents-architecture`

**Propósito**  
Tomada de decisão arquitetural e requisitos de produção para agentes de IA e sistemas multi-agente em ambientes de alta criticidade.

**Quando usar**  
- Projetar ou revisar workflows agenticos  
- Decidir se um agente é necessário vs um workflow determinístico  
- Orquestração multi-agente  
- Design de tools para agentes  
- Qualquer sistema com side effects em Core financeiro

**Estrutura (Progressive Disclosure)**

```
ai-agents-architecture/
├── SKILL.md                    # Ponto de entrada leve
├── core-constraints.md         # Regras de produção não-negociáveis
├── patterns/
│   ├── when-to-use-agent.md
│   └── shared-memory-kg.md     # Knowledge Graph como memória compartilhada persistente
├── production/
│   ├── resilience.md
│   ├── observability-audit.md
│   └── evaluation.md
└── references/
    ├── anthropic-patterns.md
    ├── andrew-ng-patterns.md
    ├── openai-multiagent.md
    └── code-examples.md
```

**Conceitos-chave**
- Preferir o padrão mais simples que atenda aos critérios de sucesso medidos.
- Knowledge Graph como memória compartilhada, persistente e com proveniência (Orchestrator-Workers + Evaluator-Optimizer).
- Orientação explícita de armazenamento na AWS (DynamoDB preferencial, Aurora PostgreSQL, Neptune apenas quando justificado).
- Checklist completo de produção para sistemas zero-downtime.

### 2. `karpathy-code-implementation`

**Propósito**  
Disciplina derivada de Karpathy para escrever e editar código que um engenheiro sênior respeitaria sem reescrever.

**Quando usar**  
- Produzir, revisar, refatorar ou debugar código-fonte real  
- Feature branches, pull requests, merges  
- Detalhes de implementação

**Estrutura (Progressive Disclosure)**

```
karpathy-code-implementation/
├── SKILL.md                    # Ponto de entrada leve
├── principles.md               # Princípios detalhados + self-critique
├── failure-modes.md            # Kitchen Sink, Optimistic Path, etc.
└── examples/
    └── code-examples.md        # Exemplos em Python, Java, Go
```

**Princípios centrais (condensados)**
- Read Before You Write
- Think Before You Code
- Simplicity First
- Surgical Changes
- Goal-Driven Execution + Empirical Verification

## Como essas skills trabalham juntas

| Preocupação                         | Skill                          |
|-------------------------------------|--------------------------------|
| Devo usar um agente?                | `ai-agents-architecture`       |
| Restrições de produção (Core)       | `ai-agents-architecture`       |
| Memória compartilhada / Knowledge Graph | `ai-agents-architecture`   |
| Qualidade de código e diffs         | `karpathy-code-implementation` |
| Self-critique antes de entregar     | `karpathy-code-implementation` |

Ao gerar código para sistemas Core, **ambas as skills devem estar ativas**.

---

## Exemplos de Uso

### Exemplo 1 — Decisão arquitetural (usar ou não agente)

**Prompt do usuário:**
> Preciso processar conciliações PIX que chegam de múltiplas fontes e podem ter inconsistências. Devo criar um multi-agente?

**Comportamento esperado com `ai-agents-architecture`:**
1. A skill força a pergunta: “O fluxo é determinístico o suficiente para um workflow simples?”
2. Carrega `patterns/when-to-use-agent.md`.
3. Se a resposta for “não”, rejeita multi-agente e sugere um workflow com circuit breaker + idempotência.
4. Se a resposta for “sim”, exige que `core-constraints.md` seja aplicado (idempotency keys, audit trail, human-in-the-loop em ações de alto risco).

### Exemplo 2 — Implementação de código com side-effect

**Prompt do usuário:**
> Implemente a função que debita a conta e registra a liquidação.

**Comportamento esperado com ambas as skills ativas:**
- `ai-agents-architecture` exige: idempotency key, circuit breaker, timeout, audit log e least privilege.
- `karpathy-code-implementation` exige: leitura do código existente, diff mínimo (surgical), sem abstração prematura, self-critique antes de apresentar.
- O resultado final deve passar no checklist de `core-constraints.md` + princípios de simplicidade e verificação empírica.

### Exemplo 3 — Revisão de Pull Request

**Prompt do usuário:**
> Revise este PR que adiciona um novo agente de conciliação.

**Fluxo esperado:**
1. `ai-agents-architecture` verifica se o agente era realmente necessário e se as restrições de Core foram respeitadas.
2. `karpathy-code-implementation` analisa o diff: tamanho, estilo, failure modes (Kitchen Sink, Optimistic Path, etc.).
3. A resposta combina feedback arquitetural + feedback de implementação, com prioridade clara para as restrições não-negociáveis.

### Exemplo 4 — Progressive Disclosure em ação

Quando a tarefa é apenas “escrever um validador simples”, o modelo carrega **apenas**:
- `karpathy-code-implementation/SKILL.md`
- (opcionalmente) `principles.md` e `examples/code-examples.md`

Ele **não** carrega `shared-memory-kg.md` nem `production/resilience.md`, mantendo o contexto limpo.

---

## Origem e Evolução

Essas skills foram desenvolvidas de forma iterativa com as seguintes influências principais:

- Anthropic – Building Effective Agents + orientações mais recentes de context engineering (Claude 5)
- Andrew Ng – Padrões de Agentic AI + disciplina de avaliação
- Andrej Karpathy – Observações sobre modos de falha de LLMs ao escrever código
- Requisitos de produção para sistemas Core financeiros (idempotência, circuit breakers, auditabilidade, least privilege)

A arquitetura foi deliberadamente migrada de conjuntos de regras monolíticos para progressive disclosure após as orientações públicas da Anthropic sobre redução de over-constraint em modelos mais novos.

## Licença

Repositório privado. Apenas para uso interno e compartilhamento controlado.
