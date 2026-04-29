# Transformation Rules

How a standard flow voucher transforms into the approval flow voucher variants. These rules apply regardless of product (Código Cash, Préstamos, Transferencias, etc.).

## The approval flow trilogy

When a transaction requires approval, it spawns THREE voucher screens for the approvers:

1. **Autorización Completada** — shown to a signer who just signed but the quorum isn't complete
2. **Comprobante (final)** — shown when the last signer completes the quorum and the transaction executes
3. **Transacción Rechazada** — shown to everyone when any signer rejects (kills the flow)

All three share the same base transaction data from the standard flow, but transform as follows:

## Field-level transformations

### Fields that are ADDED in the approval flow (not in standard flow)

- `Sometido por` → name of the user who originated the transaction (the submitter)
- `Autorizado por` → vertical list of names of the users who must sign (and who have signed, depending on UI — usually just lists all authorizers of the transaction)

### Fields that change LABEL depending on state

The date field is the most important example:

| Standard flow voucher uses | Approval flow equivalent uses |
|---|---|
| `Fecha` | `Fecha solicitud` (on Autorización Completada) |
| `Fecha` | `Fecha aprobación` (on Comprobante final) |
| `Fecha` | `Fecha de rechazo` (on Transacción Rechazada) |

These are semantically different timestamps (see `field-label-matrix.md` for details). Do NOT just rename the field — the underlying value represents a different moment in time.

### Fields that are REMOVED in rejected state

On Transacción Rechazada, these fields are typically removed because they no longer apply:
- `Total a debitar` → nothing was debited
- `No. de referencia` → no transaction reference was generated
- `Comisión` → may or may not appear, depending on the product (often removed)
- All disclaimers about pending approval or completion
- `Descripción` does NOT appear on rejected vouchers

### Fields that are KEPT unchanged across all three approval flow vouchers

- `Tipo`
- `Beneficiario` (or `Préstamo` / equivalent)
- `Desde`
- Product-specific fields (e.g., for loans: `Cargo por saldo anticipado`, `Cargo por mora`, `Interés`, `Balance de capital`)

## Screen-level transformations

### Icon transformation

| Approval flow screen | Icon |
|---|---|
| Autorización Completada | Orange clock (pending — more signatures needed) |
| Comprobante final | Blue check (completed) |
| Transacción Rechazada | Red X (rejected) |

### Header transformation

| Approval flow screen | Header text |
|---|---|
| Autorización Completada | "Autorización Completada" |
| Comprobante final | "Comprobante" |
| Transacción Rechazada | "Transacción Rechazada" |

### Sub-message transformation

| Approval flow screen | Sub-message below amount |
|---|---|
| Autorización Completada | "Su autorización ha sido aplicada" |
| Comprobante final | "Su transacción ha sido realizada" OR product disclaimer (e.g., Código Cash's 24-hour message) |
| Transacción Rechazada | "El firmante [Name of rejector] ha rechazado esta transacción" — the name is bold in the UI |

### Disclaimer (colored box) transformation

| Approval flow screen | Disclaimer |
|---|---|
| Autorización Completada (more signatures still pending) | Yellow box — "Su transacción se completará una vez que sea aprobada por el/los usuario(s) autorizado(s)." |
| Comprobante final | Blue box — "Su transacción se ha completado por el monto indicado en el comprobante." |
| Transacción Rechazada | No disclaimer box |

### Button transformation

| Flow | Left button | Right button |
|---|---|---|
| Standard flow voucher | "Ir a mis productos" | "Nuevo [product]" |
| Any approval flow voucher | "Ir a mis productos" | "Aprobaciones" |

## Approval flow — edge case

If the transaction requires only ONE authorizer's signature, there is no "intermediate" Autorización Completada state — the single signer either approves (going straight to Comprobante final) or rejects (going to Transacción Rechazada).

The Autorización Completada screen exists specifically for the case where multiple signatures are required and the current signer's signature is not the last one.

## Multimoneda rules

Multimoneda logic applies to ANY story type (standard or approval flow) IF the product supports it AND the specific transaction involves currency exchange or foreign currency.

The rules (always identical regardless of story type):

1. **Same currency both sides (USD→USD, EUR→EUR):**
   - All amount labels display in that currency
   - No sub-amount
   - No exchange rate row

2. **Currency exchange (e.g., USD→RD, EUR→RD):**
   - Main amount: destination currency (what the transaction becomes). Blue/primary.
   - Sub-amount: source currency (what is being debited). Gray.
   - Add row `Tasa de cambio` with format: `RD$60.00 / US$1.00`

The "OTHERS CURRENCY LOGIC" block at the end of the acceptance criteria codifies this — copy the standard text from `po-style-guide.md` and adapt the product name. This complete logic applies to all comprobantes with multimoneda, including `Transacción Rechazada`; do not omit `Tasa de cambio` from a rejected story when exchange of currency applies.

## Compartir (share) rules

When a voucher is shared (screenshot exported by the user), the SHARED version of the screen differs from the in-app version in these ways:

1. No status bar (no clock, no battery, no signal bars)
2. No navigation bar (no share icon, no back button)
3. No action buttons (no "Ir a mis productos", etc.)
4. The body of the voucher is captured full-height

What fields to INCLUDE or EXCLUDE in the shared version depends on the product. The PO must specify which fields get excluded. Always ASK the user before generating a compartir variant.

Common exclusions (verify with user):
- Balance disponible in `Desde` field (for privacy)
- Internal reference fields not relevant to the recipient
- Disclaimers that only make sense in-app
