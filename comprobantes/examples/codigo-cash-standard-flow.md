# Example: Código Cash — Standard Flow → Approval Flow

This example shows a complete transformation from a standard-flow Código Cash voucher to the three approval-flow stories. Use it as a reference when generating similar cases.

## Source input

- **Product:** Código Cash (intrabank)
- **Image:** Screenshot of the standard "Comprobante" screen (bank logo + share icon top, blue check icon, header "Comprobante", amount RD$10,000.00, fields: Tipo=Código Cash, Beneficiario=Claudia Javier 782814177, Desde=Ahorro *4156, Fecha=13 may 2025 - 10:15 a.m., Comisión=RD$35.00, No. de referencia=999900001, Descripción=Line #1, blue disclaimer box, buttons "Ir a mis productos" / "Nuevo código")
- **User request:** Generate the three approval-flow stories (Autorización Completada, Comprobante final, Transacción Rechazada) for this transaction.
- **Disambiguation answers:**
  - Multimoneda: No
  - Compartir: No
  - Approval flow: Yes (user confirmed this transaction requires approval)

## Output 1: Autorización Completada

```
As an app negocios user i need a voucher screen to authorize the código cash transaction.

Acceptance criteria:

Once the user taps on "Sí" to authorize the transaction present the authorization screen

It must have the bank logo and a share icon

Present a header "Autorización Completada"

Below it should have the amount of the transfer. Ex: RD$10,000.00

Present a message "Su autorización ha sido aplicada"

Present the following information:

"Tipo" next to the type of transfer "Código Cash"

"Beneficiario" next to the name of the beneficiary and the account. Ex: "Claudia Javier 782814177" (if the name is long, the account should be below)

"Desde" next to the type and number of the debit account. Ex: "Ahorro *4156"

"Fecha solicitud" next to the date and time of the transaction. Ex: "13 may 2025 - 10:15 a.m."

"Comisión" next to the commission of the transfer. Ex: "RD$35.00"

"Total a debitar" next to the total amount. Ex: "RD$10,035.00"

"Sometido por" next to the name of the person that submitted the transaction. Ex: "Susan Smith"

"Autorizado por" and below the names of the authorizers

"Descripción" and below the description of the transfer

Present a disclaimer with the information of the approving users "Su transacción se completará una vez que sea aprobada por el/los usuario(s) autorizado(s)."

If the user taps on "usuario(s) autorizado(s)." show the pending approval users

Below present 2 options:

"Ir a mis productos" take the user to the dashboard

"Aprobaciones" take the user to the approval flow again
```

## Output 2: Comprobante final (flujo de aprobación)

```
As an app negocios user i need a voucher screen for the final approval of the código cash transaction.

Acceptance criteria:

Once the user taps on "Sí" to authorize the transaction and it is the final required signature present the comprobante screen

It must have the bank logo and a share icon

Present a header "Comprobante"

Below it should have the amount of the transfer. Ex: RD$10,000.00

Present a message "Su transacción ha sido realizada"

Present the following information:

"Tipo" next to the type of transfer "Código Cash"

"Beneficiario" next to the name of the beneficiary and the account. Ex: "Claudia Javier 782814177" (if the name is long, the account should be below)

"Desde" next to the type and number of the debit account. Ex: "Ahorro *4156"

"Fecha aprobación" next to the date and time of the transaction. Ex: "13 may 2025 - 10:15 a.m."

"Comisión" next to the commission of the transfer. Ex: "RD$35.00"

"No. de referencia" next to the payment reference. Ex: "999900001"

"Sometido por" next to the name of the person that submitted the transaction. Ex: "Susan Smith"

"Autorizado por" and below the names of the authorizers

"Descripción" and below the description of the transfer

Present a disclaimer with the message "Su transacción se ha completado por el monto indicado en el comprobante"

Below present 2 options:

"Ir a mis productos" take the user to the dashboard

"Aprobaciones" take the user to the approval flow again
```

## Output 3: Transacción Rechazada

```
As an app negocios user i need a voucher screen to reject the código cash transaction.

Acceptance criteria:

- Once the user taps on **"Rechazar"** to reject the transaction present the rejection screen

- It must have the bank logo and a share icon

- Present a red X icon

- Present a header **"Transacción Rechazada"**

- Below it should have the amount of the transfer. Ex: RD$10,000.00

- Present a message **"El firmante Roberto Rodriguez ha rechazado esta transacción"** (the name of the rejecting signer is bold)

- Present the following information:
  - **"Tipo"** next to the type of transfer **"Código Cash"**
  - **"Beneficiario"** next to the name of the beneficiary and the account. Ex: **"Claudia Javier 809-319-2015"** (if the name is long, the account should be below)
  - **"Desde"** next to the type and number of the debit account. Ex: **"Ahorro *4156"**
  - **"Fecha de rechazo"** next to the date and time of the rejection. Ex: **"13 may 2025 - 10:15 a.m."**
  - **"Sometido por"** next to the name of the person that submitted the transaction. Ex: **"Susan Smith"**
  - **"Autorizado por"** and below the names of the authorizers

- Below present 2 options:
  - **"Ir a mis productos"** take the user to the dashboard
  - **"Aprobaciones"** take the user to the approval flow again

FOLLOW THE UX/UI GUIDELINE AND BEHAVIOR IN FIGMA
```

## What changed between the input and each output

**Common transformations applied to all three outputs:**
- Added `Sometido por` field (not present in standard flow)
- Added `Autorizado por` field (not present in standard flow)
- Changed right button from "Nuevo código" to "Aprobaciones"

**Output-specific transformations:**

| Element | Autorización Completada | Comprobante final | Transacción Rechazada |
|---|---|---|---|
| Icon | Orange clock | Blue check | Red X |
| Header | "Autorización Completada" | "Comprobante" | "Transacción Rechazada" |
| Sub-message | "Su autorización ha sido aplicada" | "Su transacción ha sido realizada" | "El firmante [name] ha rechazado esta transacción" |
| Date label | `Fecha solicitud` | `Fecha aprobación` | `Fecha de rechazo` |
| No. de referencia | Not shown | Shown | Not shown |
| Total a debitar | Shown | Shown | Not shown |
| Disclaimer box | Yellow (pending) | Blue (completed) | None |
| Right button label | "Aprobaciones" | "Aprobaciones" | "Aprobaciones" |
