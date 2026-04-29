# Template: Comprobante final (flujo de aprobación)

Use this template for the final receipt screen shown to the authorizer whose signature completed the quorum — the transaction just executed.

## Story opening

```
As an app negocios user i need a voucher screen for the final approval of the <product-description> transaction.
```

Alternative (closer to the PO's phrasing for the standard voucher):

```
As an app negocios user i need a voucher screen to complete the <product-description> transaction with approval.
```

Examples:
- `As an app negocios user i need a voucher screen for the final approval of the código cash transaction.`
- `As an app negocios user i need a voucher screen to complete the loan payment option "Pago total" transaction with approval.`

## Acceptance criteria template

```
Acceptance criteria:

Once the user taps on "Sí" to authorize the transaction and it is the final required signature present the comprobante screen

It must have the bank logo and a share icon

Present a header "Comprobante"

Below it should have the amount of the transfer. Ex: RD$10,000.00

Present a message "Su transacción ha sido realizada"

<OR, if the product has a specific disclaimer like Código Cash, use that instead of the generic message. Ex: "Este código tiene una vigencia de 24 horas, puede ser retirado en cualquiera de nuestros cajeros automáticos.">

Present the following information:

"Tipo" next to the type of transfer "<product-name>"

"Beneficiario" next to the name of the beneficiary and the account. Ex: "Claudia Javier - 829-319-2015" (if the name is long, the account should be below)

"Desde" next to the type and number of the debit account. Ex: "Ahorro *4156"

"Fecha aprobación" next to the date and time of the transaction. Ex: "13 may 2025 - 10:15 a.m."

<PRODUCT-SPECIFIC FIELDS HERE>

<Other standard fields: Comisión, Total a debitar, Vía de pago, Impuestos DGII 0.15%, Entidad, Canal as applicable>

"No. de referencia" next to the payment reference. Ex: "999900001"

"Sometido por" next to the name of the person that submitted the transaction. Ex: "Susan Smith"

"Autorizado por" and below the names of the authorizers

"Descripción" and below the description of the transfer

Present a disclaimer with the message "Su transacción se ha completado por el monto indicado en el comprobante"

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

- Blue check icon above the header.
- Date label is `Fecha aprobación` — when the final signature completed the transaction (execution timestamp).
- `No. de referencia` APPEARS here — the transaction executed.
- `Sometido por` and `Autorizado por` both appear — this is an approval flow voucher.
- BLUE disclaimer box (transaction completed).
- The sub-message under the amount can be either the generic "Su transacción ha sido realizada" OR a product-specific disclaimer (like Código Cash's 24-hour notice).

## Key difference vs Comprobante sin aprobación

The non-approval "Comprobante" and the approval-flow "Comprobante" look nearly identical, with one critical difference: the approval-flow version **includes `Sometido por` and `Autorizado por`**, while the non-approval version does not. Also the date label is `Fecha aprobación` here vs `Fecha` in the non-approval variant.
