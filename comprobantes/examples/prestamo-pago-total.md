# Example: Préstamo — Pago Total

This example shows how loan-specific fields are handled in verification and voucher stories. Loans have fields not present in other products (Cargo por saldo anticipado, Cargo por mora, Interés, Balance de capital, Total a debitar), with explicit microservice field references.

## Source input

- **Product:** Pago de préstamo, option "Pago total"
- **Image:** Screenshot of the verification screen (chevron back, header "VERIFICACIÓN", amount RD$10,000.00, fields: Tipo=Pago total, Préstamo=Claudia Javier 782814177, Desde=Ahorro 702814156 Disponible RD$1,000,090,000.00, Cargo por saldo anticipado=RD$50.00, Cargo por mora=RD$0.00, Interés=RD$150.00, Balance de capital=RD$9,800.00, Total a debitar=RD$10,000.00, info line "Esta opción salda por completo el préstamo.", buttons "Cancelar" / "Continuar")
- **User request:** Generate the verification story.
- **Disambiguation answers:**
  - Multimoneda: No
  - Compartir: No
  - Approval flow: No (this is the without-approval variant)

## Output: Verification without approval

```
As an app negocios user i need a verification screen for payment loan option "Pago total" without approval.

Acceptance criteria:

It must have a chevron to go back to the form

It must have a header "VERIFICACIÓN"

Below it should have the amount of the transfer. Ex: RD$10,000.00

Present the following information:

"Tipo" next to the type of transfer "Pago total"

"Préstamo" next to the name of the beneficiary and the account. Ex: "Claudia Javier 782814177" (if the name is long, the account should be below)

"Desde" next to the type and number of the debit account and the balance. Ex: "Ahorro 702814156 Disponible RD$1,000,090,000.00"

"Cargo por saldo anticipado" this is the amount will come on the field "penalidadCancelacion" from "ms-consultaprestamo"

"Cargo por mora" this is the amount will come on the field "montoMora" from "ms-consultaprestamo"

"Interés" this is the amount will come on the field "montoInteres" from "ms-consultaprestamo"

"Balance de capital" this is the loan balance until the date

"Total a debitar" the sum of the "penalidadCancelacion", "montoMora", "montoInteres" and "Balance de capital"

Below present the following information "Esta opción salda por completo el préstamo."

Below present 2 options:

"Cancelar"

"Continuar"
```

## Key style notes from this example

1. **Loan beneficiary label is `Préstamo`, not `Beneficiario`** — this is a product-specific substitution. Loans use `Préstamo`; most other products use `Beneficiario`.

2. **Microservice field references are explicit** — the PO names both the backend field (`penalidadCancelacion`) and the source microservice (`ms-consultaprestamo`). Only do this when the knowledge is real; never fabricate.

3. **`Total a debitar` is defined as the sum** — for loan Pago total, the story explains that this field is calculated as the sum of the other fee fields + the principal balance.

4. **Product-specific info line at the bottom** — "Esta opción salda por completo el préstamo." sits above the buttons as a simple prose line, not in a colored disclaimer box.

5. **Verification screens don't show `Fecha`** — no date row in pre-submit screens.

## Variant with multimoneda

If the loan is in USD and the account is in RD (currency exchange), the story gets the `OTHERS CURRENCY LOGIC` block appended:

```
OTHERS CURRENCY LOGIC

If the account and loan are in USD to USD or EUR to EUR currency, present the following:

Present all the labels "currency" in the one that the user is doing the transaction

If the user is doing a transaction that involves an exchange of currency, present the following:

It should have the amount of the transfer. Ex: US$166.66 (EX: Loan USD)

The blue currency is where the transaction is going to

Below present the amount in RD. Ex: RD$10,000.00 (EX: Account on RD)

The gray currency is where the transaction is coming from

Present the following information:

"Tasa de cambio" next to the exchange rate. Ex: "RD$60.00 / US$1.00"
```
