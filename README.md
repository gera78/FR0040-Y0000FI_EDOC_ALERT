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

Transport of the SO10 texts: report `RSTXTRAN`, object `TEXT`, ID `ST`,
name `Y0000FI_EDOC_ALERT*`.
