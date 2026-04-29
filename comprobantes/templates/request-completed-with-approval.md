# Template: Solicitud completada (con aprobación)

Use this template for the post-submit screen shown to a user who just submitted a transaction that requires approval. The transaction is awaiting authorizer signatures.

## Story opening

```
As an app negocios user i need a completed application voucher screen for <product-description> with approval.
```

Examples:
- `As an app negocios user i need a completed application voucher screen for the código cash transaction with approval.`
- `As an app negocios user i need a completed application voucher screen for loan payment option "Pago total" with approval.`

## Acceptance criteria template

```
Acceptance criteria:

Once the user taps on "someter" and insert the token present a new screen

It must have the bank logo and a share icon

Present a header "Solicitud completada"

Below it should have the amount of the transfer. Ex: RD$10,000.00

Below the amount present the message "Su solicitud ha sido sometida"

Present the following information:

"Tipo" next to the type of transfer "<product-name>"

"Beneficiario" next to the name of the beneficiary and the account. Ex: "Claudia Javier - 829-319-2015" (if the name is long, the account should be below)

"Desde" next to the type and number of the debit account. Ex: "Ahorro *4156"

"Fecha solicitud" next to the date and time of the transaction. Ex: "13 may 2025 - 10:15 a.m."

<PRODUCT-SPECIFIC FIELDS HERE>

<Other standard fields: Comisión, Vía de pago, Impuestos DGII 0.15%, Entidad, Canal as applicable>

"Descripción" and below the description of the transfer

Present a disclaimer with the information of the approving users "Su transacción se completará una vez que sea aprobada por el/los usuario(s) autorizado(s)."

If the user taps on "usuario(s) autorizado(s)." show the pending approval users

Below present 2 options:

"Ir a mis productos" take the user to the dashboard

"Nuevo <product>" take the user to the form to make another <product>
```

## Multimoneda block (only if user confirmed multimoneda applies)

Append the standard "OTHERS CURRENCY LOGIC" block (see po-style-guide.md).

## Compartir variant (only if user confirmed compartir applies)

If compartir applies, add an acceptance criterion block describing what changes in the shared version:

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
- Date label is `Fecha solicitud` (not `Fecha`).
- `No. de referencia` does NOT appear here — the transaction hasn't executed yet (pending approval).
- Right button is "Nuevo [product]" — product-specific. E.g., "Nuevo código" for Código Cash, "Nuevo pago" for loan payments.
