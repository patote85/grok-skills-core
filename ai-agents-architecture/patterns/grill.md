# Decision grill (grandes decisões)

Inspiração: `mattpocock/skills` grilling / grill-me. **Não** auto-invocar. Sessão sob pedido (`grill`, `grelha`, `estressa isto`) ou no fecho de um brainstorm *architectural* com lado efeito / dinheiro / prod.

Stateless quanto a código: não escreve repo até o humano confirmar entendimento partilhado. Factos = ferramentas. Decisões = humano.

## Quando usar

- Stress-test de cutover, runtime, Bot roster, PIX/hot path, full audit, “automatizar o estorno”.
- Depois do brainstorm architectural, antes de ADR final ou de código.
- O desenho já existe e cheira a premissa não examinada.

## Quando não usar

- Ajuste, review de diff, “complementa o README”, segundo lint.
- Ideia ainda sem propósito — isso é brainstorm, não grill.
- Loop para parecer rigoroso. Uma sessão; se a árvore não cabe, o scope é que é grande demais (partir).

## Mecânica (frontier)

Árvore de desenho. **Ronda** = todas as perguntas cuja pré-condição já está fechada. Não perguntar o que depende de resposta em aberto nesta ronda.

Formato:

```
❓ Qn — <título>: <corpo + opções>

➡️ recomendação (e custo: tokens / infra / HITL)
```

Depois espera. Recalcula frontier. Facto de repo/CI/docs: vai buscar; não pergunta.

Acaba quando a frontier está vazia **e** o humano diz que o entendimento é partilhado. Só então: ADR, ou recusa, ou spike barato. Sem merge, sem deploy, sem Bot novo.

## Lentes obrigatórias neste projecto

Cada ramo grande passa por:

1. Toaster — o modelo mais barato que resolve? Precisa de agente?
2. Agent-friendly — SoT, feature-map executável, constraint no CI, prova no artefacto. Não mais markdown de “review aprovado”.
3. Core constraints — idempotência, least privilege, HITL, audit. Jev gate se for juízo (`noul≥0.70` / `risk≥1.50`).
4. Quota — contexto composto, fio por outcome, conector > browser, Bot ≠ chat.

## Relação com pstack

Grill **não** substitui prove-it-works. Fecha premissas. A prova continua a ser o artefacto (teste HTTP, `make check`, `bend PROOF.bend`).
