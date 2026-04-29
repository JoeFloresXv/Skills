# Template: Transacción Rechazada

Use this template for the rejection screen shown when a signer rejects a transaction, killing the approval flow.

## Story opening

```
As an app negocios user i need a voucher screen to reject the <product-description> transaction.
```

Examples:
- `As an app negocios user i need a voucher screen to reject the código cash transaction.`
- `As an app negocios user i need a voucher screen to reject the loan payment option "Pago total" transaction.`
- `As an app negocios user i need a voucher screen to reject the loan payment option "Cuota(s) pendiente(s)" transaction.`

## Acceptance criteria template

```
Acceptance criteria:

- Once the user taps on **"Rechazar"** to reject the transaction present the rejection screen

- It must have the bank logo and a share icon

- Present a red X icon

- Present a header **"Transacción Rechazada"**

- Below it should have the amount of the transfer. Ex: RD$5,000.00

- Present a message **"El firmante Roberto Rodriguez ha rechazado esta transacción"** (the name of the rejecting signer is bold)

- Present the following information:
  - **"Tipo"** next to the loan payment option **"Cuota(s) pendiente(s)"**
  - **"Préstamo"** next to the alias of the loan and the loan number. Ex: **"Préstamo Wesley 782814156"** (if the alias is long, the loan number should be below)
  - **"Desde"** next to the type and number of the debit account. Ex: **"Ahorro *4156"**
  - **"Fecha de rechazo"** next to the date and time of the rejection. Ex: **"13 may 2025 - 10:15 a.m."**
  - **"Sometido por"** next to the name of the person that submitted the transaction. Ex: **"Susan Smith"**
  - **"Autorizado por"** and below the names of the authorizers

- Below present 2 options:
  - **"Ir a mis productos"** take the user to the dashboard
  - **"Aprobaciones"** take the user to the approval flow again

FOLLOW THE UX/UI GUIDELINE AND BEHAVIOR IN FIGMA
```

## Multimoneda block (only if user confirmed multimoneda applies)

Append the standard "OTHERS CURRENCY LOGIC" block. Rejected transactions MUST keep the complete multimoneda logic, including `"Tasa de cambio"` when there is an exchange of currency.

## Compartir variant (only if user confirmed compartir applies)

Add:

```
Shared version (when the user taps the share icon):

The shared version of the comprobante does not display the following:

- The status bar of the phone
- The bank navigation bar
- The action buttons at the bottom
- <product-specific fields the user specified as excluded>
```

## Notes

- Red X icon above the header.
- Date label is `Fecha de rechazo` — when the rejector rejected.
- **The rejector's name is bolded** in the sub-message (in the UI). In the story, this is indicated in the placeholder or noted as a styling detail.
- The rejection button is `"Rechazar"`; do NOT write `"No"` for this trigger.
- NO disclaimer box — neither yellow nor blue (the flow is dead).
- `No. de referencia` does NOT appear — no transaction executed.
- `Total a debitar` does NOT appear — nothing was debited.
- `Comisión` typically does NOT appear — no fee was charged.
- Loan-specific fee fields (`Cargo por saldo anticipado`, `Cargo por mora`, `Interés`) are usually omitted — nothing was applied.
- If the source image shows product-specific informational rows between the loan/source account/date block and `Canal`, include the applicable rows in the rejected story unless the field is explicitly excluded. Describe each row from its label and value type.
- `Sometido por` and `Autorizado por` DO appear — this captures the flow history.
- `Descripción` does NOT appear on rejected vouchers.
- Right button is "Aprobaciones" — returns to the approvals queue.

## Fields to actively exclude from the rejection screen

These standard approval-flow fields are NOT shown when the transaction is rejected:
- `Total a debitar`
- `No. de referencia`
- `Comisión`, `Comisión total`, `Impuestos DGII 0.15%` (no money moved)
- `Canal`, `Entidad` (optional — may still appear depending on product)
- `Descripción`
- Any pending-approval disclaimer or completed disclaimer
