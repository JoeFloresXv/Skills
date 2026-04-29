# Field Label Matrix

Quick-reference matrix for state-dependent labels. When in doubt about which label to use, consult this file.

## Date label matrix

The date label is NOT a cosmetic variation â€” each label represents a different real-world timestamp. Using the wrong label is a semantic error.

| Story type | Date label | What the timestamp actually represents |
|---|---|---|
| Verification (any kind) | N/A â€” no date row on verification screens | â€” |
| Solicitud completada con aprobaciÃ³n | `Fecha solicitud` | When the submitter sent the approval request |
| Comprobante sin aprobaciÃ³n (standard flow, no approval needed) | `Fecha` | When the transaction executed (submitter = executor) |
| AutorizaciÃ³n Completada | `Fecha solicitud` | When the submitter sent the approval request (NOT when the signer signed) |
| Comprobante final (approval flow) | `Fecha aprobaciÃ³n` | When the final signer's approval completed the transaction |
| TransacciÃ³n Rechazada | `Fecha de rechazo` | When the rejecting signer rejected |

### Why this matters

- `Fecha solicitud` is the timestamp that is frozen when the submitter hit "Someter". It does NOT change regardless of how many signers sign or when.
- `Fecha aprobaciÃ³n` is generated at the moment the final signature completes the quorum. It is the execution timestamp.
- `Fecha de rechazo` is generated at the moment a signer rejects. The flow dies here.
- `Fecha` (unsuffixed) is used only in the standard flow, where the submitter and the executor are the same user, so there's no ambiguity.

## Header matrix

| Story type | Screen header |
|---|---|
| Verification (with or without approval) | "VERIFICACIÃ“N" (in the nav bar, all caps) |
| Solicitud completada con aprobaciÃ³n | "Solicitud completada" |
| Comprobante sin aprobaciÃ³n (standard flow) | "Comprobante" |
| AutorizaciÃ³n Completada | "AutorizaciÃ³n Completada" |
| Comprobante final (approval flow) | "Comprobante" |
| TransacciÃ³n Rechazada | "TransacciÃ³n Rechazada" |

## Icon matrix

| Story type | Icon |
|---|---|
| Verification (any) | None |
| Solicitud completada con aprobaciÃ³n | Orange clock |
| Comprobante sin aprobaciÃ³n | Blue check |
| AutorizaciÃ³n Completada | Orange clock |
| Comprobante final (approval flow) | Blue check |
| TransacciÃ³n Rechazada | Red X |

## Disclaimer box matrix

| Story type | Box color | Message |
|---|---|---|
| Verification with approval | Yellow | "Su transacciÃ³n se completarÃ¡ una vez que sea aprobada por el/los usuario(s) autorizado(s)." |
| Verification without approval | None | â€” (no box; may have a simple info line like "Esta opciÃ³n salda por completo el prÃ©stamo.") |
| Solicitud completada con aprobaciÃ³n | Yellow | "Su transacciÃ³n se completarÃ¡ una vez que sea aprobada por el/los usuario(s) autorizado(s)." |
| Comprobante sin aprobaciÃ³n | Blue | "Su transacciÃ³n se ha completado por el monto indicado en el comprobante." |
| AutorizaciÃ³n Completada (more signers pending) | Yellow | "Su transacciÃ³n se completarÃ¡ una vez que sea aprobada por el/los usuario(s) autorizado(s)." |
| Comprobante final (approval flow) | Blue | "Su transacciÃ³n se ha completado por el monto indicado en el comprobante." |
| TransacciÃ³n Rechazada | None | â€” (no disclaimer box) |

## Button matrix

| Story type | Left button | Right button |
|---|---|---|
| Verification without approval | "Cancelar" | "Continuar" |
| Verification with approval | "Cancelar" | "Someter" |
| Solicitud completada con aprobaciÃ³n | "Ir a mis productos" | "Nuevo [product]" |
| Comprobante sin aprobaciÃ³n | "Ir a mis productos" | "Nuevo [product]" |
| AutorizaciÃ³n Completada | "Ir a mis productos" | "Aprobaciones" |
| Comprobante final (approval flow) | "Ir a mis productos" | "Aprobaciones" |
| TransacciÃ³n Rechazada | "Ir a mis productos" | "Aprobaciones" |

The `[product]` placeholder is replaced with the product-specific noun:
- CÃ³digo Cash: "Nuevo cÃ³digo"
- Pago prÃ©stamo: "Nuevo pago"
- Transferencia: "Nueva transferencia"

## Sub-message matrix (text below the main amount)

| Story type | Sub-message |
|---|---|
| Verification (any) | None |
| Solicitud completada con aprobaciÃ³n | "Su solicitud ha sido sometida" (or product disclaimer like CÃ³digo Cash 24-hour message) |
| Comprobante sin aprobaciÃ³n | Product disclaimer if applicable, otherwise none |
| AutorizaciÃ³n Completada | "Su autorizaciÃ³n ha sido aplicada" |
| Comprobante final (approval flow) | "Su transacciÃ³n ha sido realizada" (or product disclaimer) |
| TransacciÃ³n Rechazada | "El firmante [rejector name] ha rechazado esta transacciÃ³n" |

## Presence matrix â€” which fields appear in which story type

Legend: âœ“ = always / often appears. â€” = does not appear. * = conditional (depends on product or variant).

| Field | Verif. | Solicitud c/aprob. | Comprobante s/aprob. | Aut. Completada | Comprobante final | Rechazada |
|---|---|---|---|---|---|---|
| Tipo | âœ“ | âœ“ | âœ“ | âœ“ | âœ“ | âœ“ |
| Beneficiario | âœ“ | âœ“ | âœ“ | âœ“ | âœ“ | âœ“ |
| Beneficiarios (plural) | * | * | * | * | * | * |
| Desde | âœ“ | âœ“ | âœ“ | âœ“ | âœ“ | âœ“ |
| Fecha / variants | â€” | Fecha solicitud | Fecha | Fecha solicitud | Fecha aprobaciÃ³n | Fecha de rechazo |
| ComisiÃ³n | âœ“ | âœ“ | âœ“ | âœ“ | âœ“ | * |
| Total a debitar | âœ“ | âœ“ | âœ“ | âœ“ | âœ“ | â€” |
| No. de referencia | â€” | â€” | âœ“ | â€” | âœ“ | â€” |
| Tasa de cambio | Multi only | Multi only | Multi only | Multi only | Multi only | Multi only |
| Entidad | * | * | * | * | * | * |
| Canal | â€” | * | âœ“ | * | âœ“ | â€” |
| Sometido por | â€” | â€” | â€” | âœ“ | âœ“ | âœ“ |
| Autorizado por | â€” | â€” | â€” | âœ“ | âœ“ | âœ“ |
| DescripciÃ³n | * | * | * | * | * | * |

Notes:
- "Autorizado por" is the marker field distinguishing approval flow from standard flow.
- "No. de referencia" only appears AFTER the transaction executed (never in verification or intermediate states).
- For `TransacciÃ³n Rechazada`, `Tasa de cambio` appears when multimoneda exchange applies.
- `DescripciÃ³n` does NOT appear on `TransacciÃ³n Rechazada`.
- Loan-specific fields (Cargo por saldo anticipado, Cargo por mora, InterÃ©s, Balance de capital) appear when the product is Pago de prÃ©stamo.
