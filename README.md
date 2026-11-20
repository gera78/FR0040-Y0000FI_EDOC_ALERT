# FR0040 - Y0000FI_EDOC_ALERT

E-mail alert for French eDocuments (SAP DRC) that are not completed.
Change task: CTASK0111324.

| File | Content |
|---|---|
| `Y0000FI_EDOC_ALERT.txt` | Alert report. Original code kept; changes marked `CTASK0111324` |
| `Y0000FI_EDOC_ALERT_SO10.txt` | Report that creates the SO10 texts (subject and body) |
| `Y0000FI_EDOC_ALERT_SO10_TEXTS.txt` | Content of the SO10 texts `Y0000FI_EDOC_ALERT_SUBJECT` and `Y0000FI_EDOC_ALERT_BODY` |

The e-mail subject and body come from SO10 standard texts (ID `ST`) in the
language chosen on the selection screen (`P_LANGU`). In the body, the line
with `&EDOC_LIST&` is replaced by the list of eDocuments.

Distribution channel (`SO_VTWEG`): read from the billing document (`VBRK-VTWEG`)
through the eDocument Source Key, as `EDOC_COCKPIT` does. FI postings have no
channel; select them with option `=` and an empty value. One batch job, one
step (variant) per recipient group:

| Variant | `SO_VTWEG` | Recipient |
|---|---|---|
| Pharma | `= 32` | FactureElectroniqLaboEucerin@Beiersdorf.com |
| Mass market | `= 11`, `= 50` | FacturationElectroniqBDFNIVEA@Beiersdorf.com |
| FI postings | `=` (empty) | SSCAR0040France@Beiersdorf.com |

Transport of the SO10 texts: report `RSTXTRAN`, object `TEXT`, ID `ST`,
name `Y0000FI_EDOC_ALERT*`.

## Open items

- Link from the eDocument GUID in the ALV to `EDOC_COCKPIT` (filtered on the
  eDocument): needs the technical names of the `EDOC_COCKPIT` selection-screen
  fields (company code, source key / eDocument).
- Only red eDocuments ("Action required") in the e-mail: needs the values of
  domain `EDOC_METASTATUS` and business confirmation.
- PPF Status (table `EDOFREINV`) in the e-mail and the ALV: needs the field name.
- E-mail subject longer than 50 characters: shorten it in SO10 or send with
  `CL_BCS` + `set_message_subject`.
- Reconciliation: 1827 eDocuments without channel filter vs 852 in the three
  e-mails - check other channels / eDocument types.
