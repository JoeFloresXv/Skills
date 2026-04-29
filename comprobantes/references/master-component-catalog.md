# Master Component Catalog

Exhaustive inventory of every field that can appear in an App BIZ voucher screen. Not every voucher has every field — this catalog documents what's POSSIBLE. Each story selects the relevant subset.

## Top-of-screen elements

### Navigation bar

Two mutually exclusive patterns:

**Pattern A — Receipt/voucher screens (post-submit):**
- Bank logo centered
- Share icon (top-right, opens native share sheet)
- No back chevron
- Used for: Comprobante, Solicitud completada, Autorización Completada, Comprobante final, Transacción Rechazada

**Pattern B — Verification screens (pre-submit):**
- Back chevron (top-left, returns to the form)
- Screen title "VERIFICACIÓN" centered (all caps)
- No bank logo
- No share icon
- Used for: Verification with approval, Verification without approval

### Status icon (under the nav bar, centered)

Three possible icons — the icon encodes the state:

- **Clock icon (orange)** — pending/intermediate state. Used for: Solicitud completada con aprobación, Autorización Completada.
- **Check icon (blue circle)** — completed state. Used for: Comprobante sin aprobación, Comprobante final del flujo de aprobación.
- **X icon (red circle)** — rejected state. Used for: Transacción Rechazada.
- **No icon** — verification screens (pre-submit, no state yet).

### Screen header (h1)

The large text below the status icon. Each story type has a fixed header:

| Story type | Header |
|---|---|
| Verification (any) | Shown in nav bar as "VERIFICACIÓN" — no body header |
| Solicitud completada con aprobación | "Solicitud completada" |
| Comprobante sin aprobación | "Comprobante" |
| Autorización Completada | "Autorización Completada" |
| Comprobante final (approval flow) | "Comprobante" |
| Transacción Rechazada | "Transacción Rechazada" |

### Main amount (h1)

Large bold text. Format: `RD$10,000.00`. Always the primary transaction currency.

### Sub-amount (secondary currency — multimoneda only)

Below the main amount in smaller gray text. Format: `RD$10,000.00` or `US$166.66`.

Only present when the transaction involves currency exchange. The rules apply to every comprobante with multimoneda, including rejected vouchers:
- Main amount = currency where the transaction is going TO (the destination). Blue/primary color.
- Sub-amount = currency where the transaction is coming FROM (the source). Gray.
- Include `Tasa de cambio` when the transaction involves exchange of currency.

### Sub-message (below the amounts)

Optional text. Three possible variants:

1. **State message** (small gray text):
   - "Su solicitud ha sido sometida" → Solicitud completada con aprobación
   - "Su autorización ha sido aplicada" → Autorización Completada
   - "Su transacción ha sido realizada" → Comprobante final (approval flow)
   - "El firmante [Name] ha rechazado esta transacción" → Transacción Rechazada (the name is bold)

2. **Product-specific disclaimer** (small gray text):
   - Código Cash: "Este código tiene una vigencia de 24 horas, puede ser retirado en cualquiera de nuestros cajeros automáticos."
   - (Other products may have their own — check with the user if unsure)

3. **No sub-message** — some simple vouchers skip this

State messages and product disclaimers can co-exist OR one replace the other depending on the screen — check templates for the specific rule per story type.

## Detail rows (the field list)

Rows have two layouts:
- **Side-by-side**: label on the left, value on the right, separated by horizontal rule below. Default.
- **Stacked**: label on its own line, value below. Used for "Descripción" and "Autorizado por".

### The complete field catalog

| Field label (Spanish) | Story types where it appears | Value description |
|---|---|---|
| `Tipo` or `Tipo de transacción` | All | Product/transaction type (e.g., "Código Cash", "Pago total") |
| `Beneficiario` | All | Name + account/phone of recipient. "Claudia Javier - 829-319-2015" or "Claudia Javier 782814177". If name is long, account goes below on a new line. |
| `Beneficiarios` (plural, tappable) | Código Cash when multiple codes | Count in blue/tappable text, e.g., "10 códigos". Taps to expand the list. |
| `Préstamo` | Loan payments | Alternative to Beneficiario for loan products. Same format. |
| `Desde` | All | Source account type + number + available balance. "Ahorro *4156" in final vouchers (masked). "Ahorro 702814156 Disponible RD$1,000,090,000.00" in verification screens (full number + balance). |
| `Fecha` | Standard flow without approval | Transaction timestamp. "13 may 2025 - 10:15 a.m." |
| `Fecha solicitud` | Flows where the request timestamp matters (approval pending) | When the submitter sent the request. |
| `Fecha aprobación` | Comprobante final (approval flow) | When the final signer approved. |
| `Fecha de rechazo` | Transacción Rechazada | When the rejector rejected. |
| `Cargo por saldo anticipado` | Loan — Pago total | Value from `penalidadCancelacion` field of `ms-consultaprestamo` microservice. |
| `Cargo por abono anticipado` | Loan - Abono a capital | Fee/charge amount for an early principal payment. Include when visible in the screenshot. |
| `Monto a abonar` | Loan - Abono a capital | Principal amount the user is paying toward the loan. Include when visible in the screenshot. |
| `Cargo por mora` | Loan payments | Value from `montoMora` field of `ms-consultaprestamo`. |
| `Interés` | Loan payments | Value from `montoInteres` field of `ms-consultaprestamo`. |
| `Balance de capital` | Loan payments | The loan principal balance until the date. |
| `Comisión` | Transfers, Código Cash | Fee charged. "RD$35.00" |
| `Comisión total` | Código Cash (multiple codes) | Total fees when multiple codes issued. "RD$9,000.10" |
| `Total a debitar` | All with fees | Sum of principal + fees + taxes. |
| `Tasa de cambio` | Multimoneda only | Exchange rate used. "RD$60.00 / US$1.00" |
| `Vía de pago` | Transfers, Código Cash | Payment network. "Interbancaria" |
| `Impuestos DGII 0.15%` | All with tax | Tax amount. "RD$8.03" |
| `Entidad` | Transfers, Código Cash | Destination bank name. "Banco Popular Dominicano, S.A." |
| `Canal` | Post-transaction vouchers | Origination channel. "App BIZ" |
| `No. de referencia` or `Número de referencia` | Completed transactions only (post-execution) | Transaction reference. "999900001". NEVER appears in verification or solicitud completada screens — only appears after the transaction actually executed. |
| `Sometido por` | Approval flow only | Name of the user who originated the transaction. "Susan Smith" |
| `Autorizado por` | Approval flow only | Vertical list of authorizer names. This is the marker field: if present → approval flow; if absent → standard flow. |
| `Descripción` | When description provided | Free text. Label is bold, value on next line below. |

IMPORTANT UPDATE: `Descripción` does NOT appear on `Transacción Rechazada` vouchers.

IMPORTANT UPDATE: If a screenshot includes a field not listed in this catalog, include it in the story instead of omitting it. Any visible row between the product/loan section and `Canal` is product-specific information and must be carried into the generated story in the same order. Describe the field from its label and value type.

IMPORTANT UPDATE FOR LOAN FIELDS: Analyze field labels in loan context. `Mora` or `Cargo por mora` is the late payment fee amount. `Interés` is the interest amount of the loan payment. `Balance de capital` is the principal balance amount of the loan. Do not describe these as generic amounts.

IMPORTANT UPDATE FOR ABONO A CAPITAL: Analyze the amount relationships. The large amount below `Comprobante` is the amount the user typed in the text field. `Monto a abonar` is that same principal amount. `Cargo por abono anticipado` or `Cargo por saldo anticipado` is the penalty/charge applied for paying before time. `Total a debitar` is the amount debited from the source account, including the user-entered amount plus the charge.

## Footer elements

### Informational disclaimer (small gray text)

Product-specific info that appears between the fields and the action disclaimer. Examples:

- Código Cash: "Este monto será debitado sólo si el código es redimido, la comisión por código es de RD$35.00"
- ACH transfers: "Las transferencias realizadas a través de la red ACH entre las 8:01 a.m. y 1:00 p.m. serán acreditadas a partir de las 2:30 p.m., y las efectuadas después de las 1:00 p.m. serán acreditadas el siguiente día laborable."

These are product-dependent and appear as additional prose, not as labeled fields.

### Action disclaimer (colored box)

Two mutually exclusive variants — the color encodes the state:

**Yellow box (pending authorization):**
- Icon: orange warning/info circle
- Message: "Su transacción se completará una vez que sea aprobada por el/los usuario(s) autorizado(s)."
- The phrase "usuario(s) autorizado(s)" is underlined and tappable — shows the list of pending authorizers
- Appears when: the transaction has pending signatures
- Story types: Verification with approval, Solicitud completada con aprobación, Autorización Completada (when more signatures are needed)

**Blue box (completed):**
- Icon: blue info circle
- Message: "Su transacción se ha completado por el monto indicado en el comprobante."
- Appears when: the transaction fully executed
- Story types: Comprobante sin aprobación, Comprobante final (approval flow)

### Action buttons (bottom of screen)

Always 2 buttons, side-by-side. Left button is secondary (outlined), right button is primary (filled).

**Verification screens:**
- Left: "Cancelar"
- Right: "Someter" (with approval) OR "Continuar" (without approval — triggers token flow next)

**Standard flow vouchers:**
- Left: "Ir a mis productos" → navigates to the dashboard
- Right: "Nuevo [product]" → navigates to the form for a new transaction. Examples: "Nuevo código", "Nuevo pago", "Nueva transferencia"

**Approval flow vouchers (Autorización Completada, Comprobante final, Transacción Rechazada):**
- Left: "Ir a mis productos" → dashboard
- Right: "Aprobaciones" → returns to the approvals queue/flow

## Layout rules that apply across all voucher types

1. **Long beneficiary names** wrap: the name stays on the first line, account number drops to the second line below the name (not side-by-side).
2. **Account masking**: `Desde` shows the full account number in verification screens, but masks it to `*<last4>` in completed voucher screens.
3. **Tappable elements** are rendered in the bank's accent blue color with a chevron (`>`) if they lead somewhere. Examples: `Beneficiarios 10 códigos`, the yellow disclaimer, the `usuario(s) autorizado(s)` link inside it.
4. **Field rows render with a horizontal divider** below them (not part of story spec, just a visual detail — mention only if the PO mentions it).
