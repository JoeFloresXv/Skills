# Template: Verification (without approval)

Use this template when the story is for the pre-submit verification screen shown when the transaction does NOT require authorizer signatures (the user is about to submit it themselves).

## Story opening

```
As an app negocios user i need a verification screen for <product-description> without approval.
```

Examples:
- `As an app negocios user i need a verification screen for payment loan option "Pago total" without approval.`
- `As an app negocios user i need a verification screen for the código cash transaction without approval.`

## Acceptance criteria template

```
Acceptance criteria:

It must have a chevron to go back to the form

It must have a header "VERIFICACIÓN"

Below it should have the amount of the transfer. Ex: RD$10,000.00

Present the following information:

"Tipo" next to the type of transfer "<product-name>"

"Beneficiario" next to the name of the beneficiary and the account. Ex: "Claudia Javier - 829-319-2015" (if the name is long, the account should be below)

"Desde" next to the type and number of the debit account and the balance. Ex: "Ahorro 702814156 Disponible RD$1,000,090,000.00"

<PRODUCT-SPECIFIC FIELDS HERE>

<Other standard fields: Comisión, Vía de pago, Impuestos DGII 0.15%, Entidad, Canal as applicable>

<Optional product-specific info line, e.g., "Esta opción salda por completo el préstamo." for Pago total>

Below present 2 options:

"Cancelar"

"Continuar"
```

## Multimoneda block (only if user confirmed multimoneda applies)

Append at the end:

```
**OTHERS CURRENCY LOGIC**

If the account and loan are in USD to USD or EUR to EUR currency, present the following:

- Present all the labels **"currency"** in the one that the user is doing the transaction

If the user is doing a transaction that involves an exchange of currency, present the following:

- It should have the amount of the transfer. Ex: US$166.66 (EX: Loan USD)
  - The blue currency is where the transaction is going to

- Below present the amount in RD. Ex: RD$10,000.00 (EX: Account on RD)
  - The gray currency is where the transaction is coming from

- Present the following information:
  - **"Tasa de cambio"** next to the exchange rate. Ex: **"RD$60.00 / US$1.00"**

```

## Notes

- No yellow disclaimer box — this is the without-approval variant.
- Right button is "Continuar" (not "Someter") — triggers the token step next.
- Short product info lines (like "Esta opción salda por completo el préstamo.") go above the buttons, not in a colored box.
