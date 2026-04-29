# Template: Comprobante (sin aprobación)

Use this template for the post-submit receipt screen shown when the transaction did NOT require approval — the submitter was also the executor.

## Story opening

```
As an app negocios user i need a voucher screen for <product-description> without approval.
```

Or the PO's alternative phrasing:

```
As an app negocios user i need a completed application voucher screen for <product-description> without approval.
```

Examples:
- `As an app negocios user i need a voucher screen for the código cash transaction without approval.`
- `As an app negocios user i need a completed application voucher screen for loan payment option "Pago total" without approval.`

## Acceptance criteria template

```
Acceptance criteria:

Once the user taps on "continuar" and insert the token present a new screen

It must have the bank logo and a share icon

Present a header "Comprobante"

Below it should have the amount of the transfer. Ex: RD$10,000.00

<Optional: product-specific disclaimer below the amount, in small gray text. Ex: Código Cash — "Este código tiene una vigencia de 24 horas, puede ser retirado en cualquiera de nuestros cajeros automáticos.">

Present the following information:

"Tipo" next to the type of transfer "<product-name>"

"Beneficiario" next to the name of the beneficiary and the account. Ex: "Claudia Javier - 829-319-2015" (if the name is long, the account should be below)

"Desde" next to the type and number of the debit account. Ex: "Ahorro *4156"

"Fecha" next to the date and time of the transaction. Ex: "13 may 2025 - 10:15 a.m."

<PRODUCT-SPECIFIC FIELDS HERE>

<Other standard fields: Comisión, Vía de pago, Impuestos DGII 0.15%, Entidad, Canal as applicable>

"No. de referencia" next to the payment reference. Ex: "999900001"

"Descripción" and below the description of the transfer

Present a disclaimer with the message "Su transacción se ha completado por el monto indicado en el comprobante"

Below present 2 options:

"Ir a mis productos" take the user to the dashboard

"Nuevo <product>" take the user to the form to make another <product>
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

- Blue check icon above the header.
- Date label is `Fecha` (unsuffixed — submitter = executor, no ambiguity).
- `No. de referencia` DOES appear here — the transaction executed and generated a reference.
- NO `Autorizado por` or `Sometido por` — these are approval-flow-only fields.
- Blue disclaimer box at the bottom (not yellow).
