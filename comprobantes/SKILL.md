---
name: comprobante-story-writer
description: Writes App BIZ transaction voucher/receipt user stories (comprobantes) in the exact style of the Product Owner. Use this skill whenever the user uploads an image of a voucher screen and asks for a story, or mentions "comprobante", "voucher", "verificación", "autorización completada", "transacción rechazada", "flujo de aprobación", "solicitud completada", or asks for a story for Código Cash, Préstamos, Transferencias, or any other App BIZ transactional product. Covers both the standard transaction flow and the approval flow (where company admin users authorize, approve, or reject transactions submitted by other users). Also trigger when the user asks for multiple variants of a voucher story (e.g., "dame las 3 del flujo de aprobación") or when migrating a standard-flow voucher to its approval-flow counterparts.
---

# Comprobante Story Writer

Generate App BIZ voucher/receipt user stories in the Product Owner's exact writing style, from an image of the target screen.

## What this skill does

The user uploads an image of an App BIZ comprobante (voucher/receipt screen) and asks for a user story of a specific type. This skill produces the story in the PO's exact writing style (English narrative with Spanish UI field labels in quotes), plus a Jira-ready acceptance criteria checklist.

The skill is product-agnostic — it works for Código Cash, Préstamos (loan payments), Transferencias, ACH, and any other App BIZ transactional product.

## Story types this skill generates

There are **two flows**, each with several screen types:

**Standard flow** (a single user submits and completes a transaction):
- Verification (with approval) — pre-submit preview when the transaction requires authorization
- Verification (without approval) — pre-submit preview when the transaction does NOT require authorization
- Request completed (with approval) — post-submit screen shown when the transaction awaits authorizer signatures
- Voucher without approval — final receipt for a transaction that did not require approval

**Approval flow** (an admin/authorizer user signs, approves, or rejects a transaction submitted by someone else):
- Authorization Completed — this authorizer signed, but more signatures are pending (intermediate state)
- Final voucher (approval flow) — last authorizer signed, the transaction executed
- Rejected transaction — a signer rejected the transaction, killing the flow

Every type has possible variants:
- Multimoneda (USD-USD, EUR-EUR, or currency exchange) — opt-in, not all products support this
- Single / compartir (shareable version with reduced fields) — opt-in, product-dependent

## Workflow

**Step 1: Identify the story type requested.**

If the user clearly asks for one specific type (e.g., "crea la historia del comprobante sin aprobación"), use that.

If the user passes a standard-flow voucher and asks for "las del flujo de aprobación" without specifying which, ask which of the three they want (Autorización Completada, Comprobante final, Transacción Rechazada, or all three).

**Step 2: Ask the three disambiguation questions, ALWAYS, before generating.**

Use the `ask_user_input_v0` tool with all three in a single call:

1. **Multimoneda:** "¿Este comprobante requiere lógica multimoneda (USD-USD, EUR-EUR, o con tasa de cambio)?" — options: Sí / No
2. **Compartir:** "¿Este comprobante tiene variante de compartir (single/share)?" — options: Sí / No. If Sí, follow up asking which fields are excluded in the shared version.
3. **Aprobación (only if ambiguous from context):** "¿La transacción original requiere flujo de aprobación?" — options: Sí / No. Skip this one if the image or user request already makes it unambiguous (e.g., the image clearly shows "Autorizado por" with names).

Do not generate until the user answers.

**Step 3: Read the relevant reference and template files.**

Before writing, read these in order:

1. `references/po-style-guide.md` — the PO's writing style DNA (tone, field label conventions, acceptance criteria phrasing, examples)
2. `references/master-component-catalog.md` — the exhaustive inventory of fields that can appear in any voucher, with their exact Spanish labels and their rules
3. `references/transformation-rules.md` — rules for how fields, icons, headers, messages, disclaimers, and buttons change between standard flow and approval flow, and between states within the approval flow
4. `references/field-label-matrix.md` — the matrix that dictates which date label (`Fecha`, `Fecha solicitud`, `Fecha aprobación`, `Fecha de rechazo`) applies per story type, and other state-dependent labels
5. `templates/<story-type>.md` — the skeleton template for the exact story type requested

**Step 4: Extract fields from the uploaded image.**

Identify from the image: the product type (what goes in "Tipo"), the beneficiary or loan, the source account, the amounts (main amount, commission, total, etc.), any disclaimers, and any product-specific text (like the Código Cash 24-hour disclaimer).

IMPORTANT: Extract every visible field row between the product/loan block and `"Canal"` and carry those rows into the generated story in the same order, unless the target state explicitly removes that exact field. Do not limit the story to the known catalog fields. When a new field appears, analyze the first meaningful word in the label under the context of the transaction type and describe what the field means, not just its value type.

For loan payments, use loan-context descriptions:
- `"Mora"`: `next to the late payment fee amount. Ex: **"RD$10,800.00"**`
- `"Interés"`: `next to the interest amount of the loan payment. Ex: **"RD$10,000.00"**`
- `"Balance de capital"`: `next to the principal balance amount of the loan. Ex: **"RD$1,000,000.00"**`
- `"Cargo por saldo anticipado"` / `"Cargo por abono anticipado"`: `next to the amount charged to the user for paying before time. Ex: **"RD$3,000.00"**`
- `"Monto a abonar"`: `next to the amount the user entered to pay toward the loan. Ex: **"RD$100,000.00"**`
- `"Total a debitar"`: `next to the total amount to debit. Ex: **"RD$100,200.00"**`
- `"Impuestos DGII 0.15%"`: `next to the tax amount. Ex: **"RD$8.03"**`
- Date labels: `next to the date and time of the transaction. Ex: **"13 may 2025 - 10:15 a.m."**`

Analyze what each amount means in the context of the product instead of copying labels mechanically. For loan payment option `"Abono a capital"`, the large amount below `"Comprobante"` is the amount the user entered in the text field, so `"Monto a abonar"` represents that same user-entered principal amount. `"Cargo por abono anticipado"` or `"Cargo por saldo anticipado"` represents the penalty/charge applied to the user for paying that amount before time. `"Total a debitar"` is the sum that will be debited from the source account, including the user-entered amount plus any applicable charge. Use that reasoning to describe each field clearly in the story.

**Step 5: Generate the story.**

Produce three artifacts in the response:

0. **The Jira title** — always provide the title before the story body using the pattern `Android/iOS Comprobante - (<transaction family> - <transaction type>) - <flow/status>`.

1. **The user story** — a markdown block starting with "As an app negocios user i need..." followed by "Acceptance criteria:" and a bulleted list. Use the PO's exact style (see style guide).
2. **The Jira-ready checklist** — a second markdown block titled "Acceptance Criteria (Jira checklist)" with each criterion on its own line prefixed by `- [ ]`, ready to paste into Jira.

Every generated story must use Jira-style bullets, bold every quoted UI label/message/button/product option/example value with markdown, and end with:

```
FOLLOW THE UX/UI GUIDELINE AND BEHAVIOR IN FIGMA
```

If the user requested multiple stories (e.g., the 3 of the approval flow), generate all of them in one response, clearly separated by headers.

## Critical behaviors to never violate

- **Always include the Jira title** — for both platforms use `Android/iOS`; for loan pending payments use `(Préstamo - Cuotas pendientes)`; for authorization completed use `Autorización pendiente`, for rejected use `Rechazada`, for final signer use `Última Aprobación`, for submitted requests use `Solicitud sometida`, and for final receipts use `Comprobante final`.

- **Bold all quoted text in the Jira story** — write quoted UI labels, headers, messages, buttons, product options, and quoted example values as `**"Tipo"**`, `**"Transacción Rechazada"**`, etc.
- **Multimoneda logic is complete for every comprobante** — if exchange of currency applies, include the blue destination amount, gray source amount, and `"Tasa de cambio"` row, including for rejected vouchers.
- **Do not drop newly visible product fields** — if the screenshot has extra rows between the product/loan rows and `"Canal"`, include them in the story using wording based on the label and value type.
- **Analyze the comprobante before writing** — infer what the amounts mean from the product flow. For `Abono a capital`, the top amount equals `"Monto a abonar"` (the amount the user typed), while `"Cargo por abono anticipado"` / `"Cargo por saldo anticipado"` is the early-payment charge, and `"Total a debitar"` is the amount debited including charges.

- **Always generate in English** — the narrative is English, but Spanish UI field labels stay in Spanish inside double quotes: `"Tipo"`, `"Beneficiario"`, `"Desde"`, `"Fecha solicitud"`, etc.
- **Field label for date is NOT interchangeable** — `Fecha` vs `Fecha solicitud` vs `Fecha aprobación` vs `Fecha de rechazo` each encode a different real-world timestamp. See `field-label-matrix.md`.
- **`Autorizado por` is the approval-flow marker field** — it only appears when the transaction went through approval. A "comprobante sin aprobación" does NOT have this field. A "comprobante final del flujo de aprobación" DOES have it.
- **Never assume multimoneda or compartir** — always ask. Not every product supports them.
- **Preserve the PO's exact quirks** — lowercase "i need", curly quotes `" "`, concrete example values (not placeholders like `<name>`), inline conditional logic as prose ("if the name is long, the account should be below"), microservice field references (e.g., `penalidadCancelacion` from `ms-consultaprestamo`) when the source is a real backend field.

## File map

```
comprobante-story-writer/
├── SKILL.md                              (this file)
├── references/
│   ├── po-style-guide.md                 (style DNA, read first every time)
│   ├── master-component-catalog.md       (all possible fields + their rules)
│   ├── transformation-rules.md           (standard flow → approval flow transforms)
│   └── field-label-matrix.md             (state-dependent labels)
├── templates/
│   ├── verification-with-approval.md
│   ├── verification-without-approval.md
│   ├── request-completed-with-approval.md
│   ├── voucher-without-approval.md
│   ├── authorization-completed.md
│   ├── final-voucher-approval-flow.md
│   └── rejected-transaction.md
└── examples/
    ├── codigo-cash-standard-flow.md      (reference inputs + outputs)
    └── prestamo-pago-total.md            (reference inputs + outputs)
```
