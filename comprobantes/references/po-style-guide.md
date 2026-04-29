# Product Owner Style Guide

This file codifies the exact writing style of the App BIZ Product Owner so generated stories feel indistinguishable from hers. Read this FIRST every time before generating a story.

## Story opening

## Jira title

Always provide the Jira title before the story body.

Title pattern:

```
Android/iOS Comprobante - (<transaction family> - <transaction type>) - <flow/status>
```

Rules:
- Use `Android/iOS` when the story applies to both platforms.
- Use `Comprobante` for voucher/comprobante screens.
- Put the transaction in parentheses. For loan pending payments, use `(Préstamo - Cuotas pendientes)`.
- Use the flow/status at the end:
  - `Autorización pendiente` for `Autorización Completada` / intermediate approval screens where more signatures are pending.
  - `Rechazada` for `Transacción Rechazada`.
  - `Última Aprobación` for the final signer approval step.
  - `Solicitud sometida` for submitted requests pending approval.
  - `Comprobante final` for the executed final approval-flow receipt.

Examples:
- `Android/iOS Comprobante - (Préstamo - Cuotas pendientes) - Autorización pendiente`
- `Android/iOS Comprobante - (Préstamo - Cuotas pendientes) - Rechazada`
- `Android/iOS Comprobante - (Préstamo - Cuotas pendientes) - Última Aprobación`

Every story starts with this exact phrase (note the lowercase "i"):

```
As an app negocios user i need a <screen-type> screen <for|to approval the> <transaction-type> transaction.
```

Variations observed in the PO's writing:
- `As an app negocios user i need a voucher screen to approval the código cash transaction.`
- `As an app negocios user i need a completed application voucher screen for loan payment option "Pago total" with approval.`
- `As an app negocios user i need a verification screen for payment loan option "Pago total" without approval.`

Pattern rules:
- Lowercase "i" in "i need" — non-negotiable, this is the PO's signature
- No comma before "i need"
- Screen type in lowercase: "voucher screen", "verification screen", "completed application voucher screen"
- Transaction type in lowercase when it's a general term: "código cash transaction"
- Transaction type in quotes when it's a specific product option: `"Pago total"`
- End of line: period, no trailing text

## Body structure

Immediately after the opening line, an empty line, then:

```
Acceptance criteria:
```

Followed by a blank line, then bulleted acceptance criteria using plain text (no markdown bullets in the source — they're rendered by Jira as bullets when pasted). In the raw story, each criterion is separated by a blank line.

IMPORTANT UPDATE: Generated Jira stories now use markdown bullets and nested bullets, matching the PO's Jira editor screenshots. Use top-level `-` bullets for main acceptance criteria and nested `  -` bullets under sections like `Present the following information:`, button groups, and currency logic.

Every story MUST end with this final line:

```
FOLLOW THE UX/UI GUIDELINE AND BEHAVIOR IN FIGMA
```

## Acceptance criteria conventions

### Phrasing rules

The PO uses imperative phrases describing what the screen must have or do:

- `It must have the bank logo and a share icon`
- `Present a header "Comprobante"`
- `Below it should have the amount of the transfer.`
- `Present the following information:`
- `Below present 2 options:`

Recurring verbs the PO uses: `present`, `have`, `show`, `take the user to`, `tap on`.

### Field listing pattern

IMPORTANT UPDATE: Anything written inside quotation marks in the generated Jira story must be bolded using markdown: `**"Texto"**`. This includes Spanish labels, headers, messages, buttons, product options, example values, and quoted backend fields. For example, write `**"Tipo"**`, `**"Cuota(s) pendiente(s)"**`, `**"Transacción Rechazada"**`, and `**"Ir a mis productos"**`.

When listing the information a screen must show, the PO uses this exact micro-pattern:

```
**"<Spanish label>"** next to the <description of value>. Ex: **"<concrete example>"**
```

Examples from the PO:
- `"Tipo de transacción" next to the type of transfer "Código cash"`
- `"Beneficiario" next to the name of the beneficiary and the account. Ex: "Claudia Javier - 829-319-2015"`
- `"Desde" next to the type and number of the debit account and the balance. Ex: "Ahorro *4156 Disponible" RD$1,000,090,000.00"`
- `"Fecha de solicitud" next to the date and time of the transaction. Ex: "10/06/2024 4:17 PM."`
- `"Comisión" next to the commission of the transfer. Ex: "RD$35.00"`

Common typo the PO makes (preserve it only if consistent): `"nest to"` instead of `"next to"` — actually, CORRECT it when generating. Do not replicate obvious typos.

### New visible fields in the screenshot

When the image shows additional field rows between the product/loan information and **"Canal"**, include those fields in the generated story in the same order. Do not ignore a field just because it is not in the template.

Describe unknown/new fields by analyzing the first meaningful word in the label under the context of the transaction. Do not default to `next to the amount` if a more specific loan meaning is available.

For loan payments:
- `**"Mora"** next to the late payment fee amount. Ex: **"RD$10,800.00"**`
- `**"Interés"** next to the interest amount of the loan payment. Ex: **"RD$10,000.00"**`
- `**"Balance de capital"** next to the principal balance amount of the loan. Ex: **"RD$1,000,000.00"**`
- `**"Cargo por saldo anticipado"** next to the amount charged to the user for paying before time. Ex: **"RD$3,000.00"**`
- `**"Cargo por abono anticipado"** next to the amount charged to the user for paying before time. Ex: **"RD$200.00"**`
- `**"Monto a abonar"** next to the amount the user entered to pay toward the loan. Ex: **"RD$100,000.00"**`
- `**"Total a debitar"** next to the total amount to debit. Ex: **"RD$100,200.00"**`
- `**"Impuestos DGII 0.15%"** next to the tax amount. Ex: **"RD$8.03"**`

For non-loan fields not covered above, infer the clearest noun phrase from the label before falling back to a generic amount description.

### Field meaning analysis

Before writing the story, analyze the comprobante as a complete transaction and infer what each amount means from the product flow. Do not describe fields only by copying their labels.

For loan payment option **"Abono a capital"**:
- The large amount below **"Comprobante"** is the amount the user typed in the amount text field.
- **"Monto a abonar"** is that same user-entered principal amount. Phrase it as: `**"Monto a abonar"** next to the amount the user entered to pay toward the loan. Ex: **"RD$100,000.00"**`
- **"Cargo por abono anticipado"** or **"Cargo por saldo anticipado"** is the penalty/charge applied because the user is paying before time. Phrase it as: `**"Cargo por abono anticipado"** next to the amount charged to the user for paying before time. Ex: **"RD$200.00"**`
- **"Total a debitar"** is the amount debited from the source account, including the amount entered by the user plus the applicable charge. Phrase it as: `**"Total a debitar"** next to the total amount to debit. Ex: **"RD$100,200.00"**`

### Conditional logic as inline prose

The PO does not use if-then blocks. She writes conditionals inline as parenthetical notes or short "if" sentences:

- `"Beneficiario" next to the name of the beneficiary and the account. Ex: "Claudia Javier - 829-319-2015" (if the name is long, the account should be below)`
- `If the user taps on "usuario(s) autorizado(s)." show the pending approval users`

### Fields "below" other fields

For fields where the label sits above the value (rather than to the side), the PO uses this pattern:

- `"Descripción" and below the description of the transfer`
- `"Autorizado por" and below the names of the authorizers`

Note: the PO says "and below" (not "with the value below") to signal vertical layout.

### Header labels — exact capitalization

The Spanish labels the PO uses appear in specific capitalizations. Preserve these exactly:

| Label (as the PO writes it) | Do NOT write |
|---|---|
| `"Tipo"` or `"Tipo de transacción"` | "TIPO", "tipo" |
| `"Beneficiario"` | "beneficiario" |
| `"Desde"` | "DESDE" |
| `"Fecha"`, `"Fecha solicitud"`, `"Fecha aprobación"`, `"Fecha de rechazo"` | "fecha" |
| `"Comisión"` | "Comision" (no missing accent) |
| `"Total a debitar"` | "Total a Debitar" |
| `"Número de referencia"` or `"No. de referencia"` | "Numero de referencia" |
| `"Impuestos DGII 0.15%"` | "Impuestos DGII 0.15" (don't drop the %) |
| `"Canal"` | "CANAL" |
| `"Descripción"` | "descripcion" |
| `"Autorizado por"` | "Autorizado Por" |
| `"Sometido por"` | "Sometido Por" |
| `"Tasa de cambio"` | "Tasa de Cambio" |
| `"Vía de pago"` | "Via de pago" |
| `"Entidad"` | "entidad" |

## Example values

Concrete, realistic examples are MANDATORY. Never use placeholders like `<amount>`, `[name]`, `{date}`. Use real-looking values:

- Amounts: `RD$10,000.00`, `US$166.66`, `RD$35.00`, `RD$8.03`, `RD$10,035.00`
- Exchange rate: `RD$60.00 / US$1.00`
- Names: `Claudia Javier`, `Susan Smith`, `Martina Jiménez`, `Braulio Gómez`, `Roberto Rodriguez`
- Accounts: `782814177`, `702814156`, `Ahorro *4156`, `829-319-2015`
- Dates: `13 may 2025 - 10:15 a.m.`, `10/06/2024 4:17 PM.`
- References: `999900001`
- Entity: `Banco Popular Dominicano, S.A.`
- Channel: `App BIZ`

Use the SAME example values the PO uses when possible — she reuses `Claudia Javier`, `Susan Smith`, `RD$10,000.00`, etc. as a kind of canonical test dataset. Reuse them for consistency.

## Currency and amount formatting

Observed patterns:
- Always prefix currency: `RD$`, `US$`, `EUR$`
- Thousands separator: comma
- Decimal separator: period
- Always two decimal places
- No space between currency and number: `RD$10,000.00` (not `RD$ 10,000.00`) — EXCEPTION: when rendered in the UI the bank uses `RD$ 35.00` with space, but in the story text the PO writes `RD$35.00` without. Prefer no space in story text.

## Microservice field references

When an acceptance criterion describes a value that comes from a specific backend field, the PO explicitly names the field and the microservice:

```
"Cargo por saldo anticipado" this is the amount will come on the field "penalidadCancelacion" from "ms-consultaprestamo"
"Cargo por mora" this is the amount will come on the field "montoMora" from "ms-consultaprestamo"
"Interés" this is the amount will come on the field "montoInteres" from "ms-consultaprestamo"
```

Pattern: `"<label>" this is the amount will come on the field "<fieldName>" from "<ms-name>"`.

Only use this pattern when you have actual knowledge of the backend field/microservice. Do not fabricate microservice names.

## Multimoneda block — "OTHERS CURRENCY LOGIC"

IMPORTANT UPDATE: This logic applies to every comprobante that has multimoneda, including rejected vouchers. Do not remove `"Tasa de cambio"` from rejected stories when the transaction involves exchange of currency.

When a story includes multimoneda variants, the PO appends this section verbatim (with minor wording variations) at the end of the acceptance criteria:

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

Replace `loan` with the relevant product term (`account`, `loan`, etc.) depending on the transaction type. Preserve the typo `exhange` only if you want to exactly mirror the PO — otherwise correct to `exchange rate`.

## Buttons section

The PO describes buttons with this pattern:

```
Below present 2 options:

"<Button 1 label>" <optional: what it does>

"<Button 2 label>" <optional: what it does>
```

Examples:
- `"Ir a mis productos" take the user to the dashboard`
- `"Aprobaciones" take the user to the form to make another transfer` (note: PO occasionally writes inconsistent descriptions — verify against design)
- `"Nuevo pago" take the user to the form to make another payment`
- `"Cancelar"` (no description)
- `"Someter"` (no description)

When the button action is obvious from its label (`Cancelar`, `Continuar`, `Someter`), the PO often omits the description.

## Disclaimers

The PO quotes disclaimer text verbatim inside the story:

- `Present a disclaimer with the message "Su transacción se ha completado por el monto indicado en el comprobante"`
- `Present a disclaimer with the information of the approving users "Su transacción se completará una vez que sea aprobada por el/los usuario(s) autorizado(s)."`
- `Below present a the following the information "Esta opción salda por completo el préstamo."` (this exact phrasing with typo "a the" appears in the PO's text — DO correct obvious typos like this)

## State-specific opening sentence after the header

Different story types have a specific second-line message shown below the amount:

- Standard voucher: no sub-message OR a product disclaimer ("Este código tiene una vigencia de 24 horas...")
- Solicitud completada con aprobación: `Present a message "Su solicitud ha sido sometida"`
- Solicitud completada con aprobación (standard flow "Comprobante" approval flow variant): `Below the amount present the message "Su solicitud ha sido sometida"`
- Autorización Completada: `Present a message "Su autorización ha sido aplicada"`
- Comprobante final approval flow: `Present a message "Su transacción ha sido realizada"`
- Rechazada: `Present a message "El firmante "Name of the person that is rejecting the transaction" ha rechazado esta transacción"`

## Trigger for the screen

Every story starts its acceptance criteria with the user action that triggers the screen. The PO writes this as a single bullet:

- `Once the user taps on "Si" to autorize the transaction present the verification screen`
- `Once the user taps on "someter" and insert the token present a new screen`
- `Once the user taps on "continuar" and insert the token present a new screen`

Note: the PO frequently misspells "autorize" (should be "authorize") and does not fix it. When generating, USE the correct English spelling. Do not replicate typos.

## What NOT to do

- Do not use markdown headers (`#`, `##`) inside the story body — the PO writes plain prose with bulleted ACs
- Do not leave quoted labels, messages, buttons, product options, or quoted example values unbolded
- Do not use numbered lists — the PO uses bulleted or plain-separated lines
- Do not use placeholder tokens (`<name>`, `[amount]`) — always use concrete examples
- Do not translate Spanish UI labels to English — labels stay in Spanish in quotes
- Do not invent microservice names or backend field names
- Do not abbreviate currency codes (`USD`, `EUR`) when the UI uses symbols (`US$`, `EUR$`)
