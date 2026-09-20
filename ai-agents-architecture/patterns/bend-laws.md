# Bend — when it is a gate, not a runtime

Do not adopt Bend 2 as the default implementation language. This file is only the routing rule.

Source: https://bend-lang.com  
Spike local: `artifacts/crud-api-bend/`  
Contrato: `LAWS.bend` (humano) + `PROOF.bend` (agente). Gate: `bend PROOF.bend`.  
Não enfraquecer lei para o proof passar.

## Default

**Não usar Bend.** Stack da casa (hoje: Python/SAM no CRUD AWS, o que o domínio já corre). Agente gera código sob `karpathy-code-implementation`.

Evidência neste projecto (sandbox, 2026-09-19): Bend CRUD ~12 TPS sem erro, ~1.6 GB RSS, timeouts a 8 workers, `persist: skip write` sob disputa. Python do mesmo contrato + moto: 300–500 TPS, ~84 MB, 800/800 a 32 workers. Paridade de contrato ≠ paridade de sistema.

## Quando carregar Bend

Só com **job concreto** que peça leis executáveis, e só no núcleo **puro** (zero socket, zero File no termo da lei):

- invariante contabilístico / de estado com dono humano das leis;
- spec que o serviço real já implementa noutro runtime;
- sandbox de agente (impedir “apaguei o teste”).

Não usar para: API pública, ledger de posição, pagamento, TLS, Dynamo, auth, carga, multi-processo.

## Relação com o agente

CRUD HTTP determinístico **não** precisa de agente dinâmico (`when-to-use-agent.md`).  
Bend também não transforma um workflow em Bot.  
Grok chat ≠ Grok Bot. Multi-bot só após um Bot com ganho medido — Bend não é esse ganho.

## Do not add to this skill pack

Guia da linguagem, tactics, demos TCP. Ficam em bend-lang.com e no spike. Copiar o guide aqui garante drift.
