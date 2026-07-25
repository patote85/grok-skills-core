# Code Examples — ai-agents-architecture

Três exemplos concretos. Código em en-US, comentários em pt-BR.  
Contexto: agentes e workflows em Core financeiro de alta criticidade.

---

## 1. Python — Workflow simples vs Agent desnecessário

```python
# Preferir workflow determinístico sempre que os passos forem conhecidos
def route_and_execute_payment(request: PaymentRequest) -> PaymentResult:
    # Roteamento explícito e auditável — sem LLM
    if request.rail == "PIX" and request.amount <= PIX_LIMIT:
        return execute_pix(request)          # side-effect com idempotency_key interno
    if request.rail == "TED":
        return execute_ted(request)
    raise UnsupportedRailError(f"rail {request.rail} not supported")

# Só escalar para agent quando a sequência de passos for imprevisível
# e houver feedback do ambiente + critério de sucesso mensurável
```

---

## 2. Java — Tool definition com risco e docstring de qualidade (ACI)

```java
/**
 * Executes a PIX transfer. HIGH RISK — moves real money.
 *
 * Use only after all business validations have passed.
 * Always supply a unique idempotencyKey.
 * Returns settlement status or throws on permanent failure.
 */
@Tool
public Map<String, Object> executePixTransfer(
        String endToEndId,
        BigDecimal amount,
        String debtorAccount,
        String creditorKey,
        String idempotencyKey) {

    // Circuit breaker + timeout + audit já encapsulados no client
    return pixClient.transfer(
        PixTransferRequest.builder()
            .endToEndId(endToEndId)
            .amount(amount)
            .debtorAccount(debtorAccount)
            .creditorKey(creditorKey)
            .idempotencyKey(idempotencyKey)
            .build()
    );
}
```

---

## 3. Go — Minimal agent loop com transparência, limite e audit

```go
const maxIterations = 8

func RunAgent(ctx context.Context, goal string, tools []Tool) (AgentResult, error) {
    messages := []Message{{Role: "system", Content: systemPrompt}, {Role: "user", Content: goal}}
    audit := make([]AuditEntry, 0, maxIterations)

    for i := 0; i < maxIterations; i++ {
        resp, err := llm.Chat(ctx, messages, tools)
        if err != nil {
            return AgentResult{}, err
        }
        audit = append(audit, AuditEntry{Iteration: i, Response: resp})

        if resp.StopReason == "end_turn" {
            return AgentResult{Success: true, Output: resp.Content, Audit: audit}, nil
        }

        for _, call := range resp.ToolCalls {
            // Gate de risco — ações de alto impacto exigem aprovação
            if isHighRisk(call.Name) {
                if !humanApproval(ctx, call) {
                    return AgentResult{Success: false, Reason: "HIGH_RISK_REJECTED", Audit: audit}, nil
                }
            }

            result := executeTool(ctx, call) // internamente usa idempotency key
            messages = append(messages, toolResultMessage(call, result))
            audit = append(audit, AuditEntry{Tool: call.Name, Result: result})
        }
    }

    return AgentResult{Success: false, Reason: "MAX_ITERATIONS", Audit: audit}, nil
}
```
