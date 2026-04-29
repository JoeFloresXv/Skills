# Template: Autorización Completada

Use this template for the intermediate-state screen shown to an authorizer who just signed a transaction, but more signatures are still pending (the quorum isn't complete).

## Story opening

```
As an app negocios user i need a voucher screen to authorize the <product-description> transaction.
```

Examples:
- `As an app negocios user i need a voucher screen to authorize the código cash transaction.`
- `As an app negocios user i need a voucher screen to authorize the loan payment option "Pago total" transaction.`
- Title example: `Android/iOS Comprobante - (Préstamo - Cuotas pendientes) - Autorización pendiente`

## Acceptance criteria template

```
Acceptance criteria:

Once the user taps on "Aprobar" to authorize the transaction present the authorization screen

It must have the bank logo and a share icon

Present a header "Autorización Completada"

Below it should have the amount of the transfer. Ex: RD$10,000.00

Present a message "Su autorización ha sido aplicada"

Present the following information:

"Tipo" next to the type of transfer "<product-name>"

"Beneficiario" next to the name of the beneficiary and the account. Ex: "Claudia Javier - 829-319-2015" (if the name is long, the account should be below)

"Desde" next to the type and number of the debit account. Ex: "Ahorro *4156"

"Fecha solicitud" next to the date and time of the transaction. Ex: "13 may 2025 - 10:15 a.m."

<PRODUCT-SPECIFIC FIELDS HERE>

<Other standard fields: Comisión, Total a debitar, Vía de pago, Impuestos DGII 0.15%, Entidad, Canal as applicable>

If the source image shows additional product-specific rows between the loan/source account/date block and "Canal", include them here in the same order. Examples for "Abono a capital":
- **"Cargo por abono anticipado"** next to the amount. Ex: **"RD$200.00"**
- **"Monto a abonar"** next to the amount. Ex: **"RD$100,000.00"**
- **"Total a debitar"** next to the total amount to debit. Ex: **"RD$100,200.00"**

"Sometido por" next to the name of the person that submitted the transaction. Ex: "Susan Smith"

"Autorizado por" and below the names of the authorizers

"Descripción" and below the description of the transfer

Present a disclaimer with the information of the approving users "Su transacción se completará una vez que sea aprobada por el/los usuario(s) autorizado(s)."

If the user taps on "usuario(s) autorizado(s)." show the pending approval users

Below present 2 options:

"Ir a mis productos" take the user to the dashboard

"Aprobaciones" take the user to the approval flow again
```

## Multimoneda block (only if user confirmed multimoneda applies)

Append the standard "OTHERS CURRENCY LOGIC" block.

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

- Orange clock icon above the header.
- The approval action button is `"Aprobar"`; do NOT write `"Sí"` for this trigger.
- Carry over every visible product-specific amount row from the source image, especially rows between `Fecha solicitud` and `Canal`.
- Date label is `Fecha solicitud` — when the submitter sent the request, not when the current signer signed.
- YELLOW disclaimer box (more signers still pending).
- `No. de referencia` does NOT appear — the transaction hasn't executed yet (still pending remaining signatures).
- This screen exists only when multiple signatures are required. If only one signature is needed, the flow skips this screen and goes straight to "Comprobante" final OR "Transacción Rechazada".
- Right button is "Aprobaciones" — sends the user back to the approvals queue, NOT to a new transaction form.
