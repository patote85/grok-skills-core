# Decision brainstorm (grandes decisões)

Inspiração: `obra/superpowers` brainstorming. **Não** copiar o trigger “MUST before any creative work”. Aqui o trigger é *decisão grande*. Ajuste de README, lint, teste, PUT parcial, complemento de tabela = Karpathy + skill de domínio. Sem este ficheiro.

Princípio: *You don’t need Newton-level intelligence in your toaster.* Tokens e infra pagam-se em cada ronda.

## Quando usar

- Novo bounded context, cutover, runtime novo, multi-bot, dinheiro/IAM/prod, “substituir X por Y”.
- O humano pede brainstorm / desenho / “vale a pena?”.
- Classificação **architectural** (não bounded, não spike de uma linha).

## Quando não usar

- Diff pequeno, CI verde, docs, prova Bend, harness Jev, feature-map de uma rota.
- Segunda opinião sobre um PR já scoped.
- Qualquer coisa que o `when-to-use-agent.md` já rejeita como agente.

## Processo (curto)

1. Classificar em voz alta: spike / bounded / architectural. Em dúvida, **não** inflacionar — spike primeiro.
2. Ler o SoT que já existe (ADR, feature-map, skills). Não perguntar facto que o repo responde.
3. Uma pergunta de intenção de cada vez (purpose, constraint, critério de sucesso). Escolhas > aberto.
4. 2–3 abordagens com custo (tokens, infra, HITL). Recomendação explícita. YAGNI.
5. Desenho em chat, secções curtas. Parar. Esperar sim.
6. Só então ADR / spec. Não scaffolding, não `npx`, não Bot.

Spike: 2–3 frases + nod + prova barata + throwaway.
Bounded: desenho no chat + sim → Karpathy. Sem spec file.
Architectural: desenho + spec + grill se o risco for dinheiro/prod/runtime.

## Anti-padrão

| Pensamento | Realidade |
|---|---|
| “Todo feature precisa disto” | Toaster. Skill de código. |
| “Aprovei a ideia, implementa” | Aprovação é do *artefacto apresentado*. |
| “O spike funcionou, fica o código” | Pedido novo. Reclassificar. |
| “11 agentes porque a U9 tem supervisor” | Um dono com ganho medido. |
