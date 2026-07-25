# Code Examples — karpathy-code-implementation

Três exemplos concretos. Código em en-US, comentários em pt-BR.  
Contexto: operações de Core financeiro (transferência, validação, side-effects).

---

## 1. Python — Simplicity First + Surgical Change

**Task:** Adicionar verificação de idempotência em função existente.

```python
def settle_transaction(tx_id: str, amount: Decimal, idempotency_key: str) -> SettlementResult:
    # Verifica se a chave de idempotência já foi processada
    if already_processed(idempotency_key):
        return get_existing_result(idempotency_key)

    # Lógica de negócio original permanece intacta (surgical)
    debit_account(tx_id, amount)
    credit_account(tx_id, amount)
    record_settlement(tx_id, amount)

    # Registra o resultado para futuras chamadas com a mesma chave
    save_idempotency_result(idempotency_key, status="SUCCESS")
    return SettlementResult(status="SUCCESS", tx_id=tx_id)
```

---

## 2. Java — Avoid Optimistic Path + Clear Validation

```java
public TransferResult transfer(String fromAccount, String toAccount, BigDecimal amount, String idempotencyKey) {
    // Validação explícita — nunca confiar apenas no happy path
    if (amount == null || amount.compareTo(BigDecimal.ZERO) <= 0) {
        throw new InvalidAmountException("amount must be positive");
    }

    // Controle de concorrência + idempotência
    try (DistributedLock lock = lockService.acquire("transfer:" + idempotencyKey)) {
        if (idempotencyStore.exists(idempotencyKey)) {
            return idempotencyStore.load(idempotencyKey);
        }

        try {
            accountService.debit(fromAccount, amount);
            accountService.credit(toAccount, amount);
            TransferResult result = TransferResult.success(idempotencyKey);
            idempotencyStore.save(idempotencyKey, result);
            return result;
        } catch (InsufficientFundsException e) {
            // Falha de negócio esperada — registra e propaga
            idempotencyStore.save(idempotencyKey, TransferResult.failed("INSUFFICIENT_FUNDS"));
            throw e;
        }
    }
}
```

---

## 3. Go — Minimal Diff + Explicit Error Handling

```go
func ProcessPayment(ctx context.Context, req PaymentRequest) (PaymentResult, error) {
    // Validação mínima e direta
    if req.Amount.LessThanOrEqual(decimal.Zero) {
        return PaymentResult{}, errors.New("amount must be positive")
    }

    // Verificação de idempotência antes de qualquer side-effect
    if existing, found := idempotency.Get(ctx, req.IdempotencyKey); found {
        return existing, nil
    }

    // Execução com tratamento explícito de erro
    if err := ledger.Debit(ctx, req.FromAccount, req.Amount); err != nil {
        return PaymentResult{}, fmt.Errorf("debit failed: %w", err)
    }

    if err := ledger.Credit(ctx, req.ToAccount, req.Amount); err != nil {
        // Compensação simples — em produção real usaria saga ou outbox
        _ = ledger.Credit(ctx, req.FromAccount, req.Amount)
        return PaymentResult{}, fmt.Errorf("credit failed: %w", err)
    }

    result := PaymentResult{Status: "SUCCESS", Key: req.IdempotencyKey}
    idempotency.Save(ctx, req.IdempotencyKey, result)
    return result, nil
}
```
