# Portfolio Activity: Phishing Alert Ticket

## Ticket details

| Field | Value |
|---|---|
| Ticket ID | A-2703 |
| Alert | SERVER-MAIL - Phishing attempt / possible malware download |
| Severity | Medium |
| Initial status | Open |
| Final status | Escalation |
| Recipient | hr@inergy.com |
| Sender display name | Clyde West |
| Sender address/domain | 76tguyhh6tgftrt7tg.su |
| Sender IP | 114.114.114.114 |
| Recipient IP shown in alert | 176.157.125.93 |
| Date and time | July 20, 2022, 09:30:14 AM |
| Subject | Re: Infrastructure Egnieer role |
| Attachment | bfsvc.exe |
| Attachment password | paradise10789 |
| SHA-256 | 54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b |

## Incident summary

A phishing alert was generated for an email sent to the HR mailbox at Inergy. The message presented itself as a job application from Clyde West and included a password-protected executable attachment named `bfsvc.exe`, described as a resume and cover letter. The attachment's SHA-256 hash was confirmed to be malicious.

## 5 Ws

- **Who:** The email claims to be from Clyde West. The intended recipient is the HR mailbox, `hr@inergy.com`.
- **What:** A suspected phishing email delivered a password-protected executable attachment, `bfsvc.exe`, whose hash is known to be malicious.
- **When:** July 20, 2022 at 09:30:14 AM, according to the email header in the alert.
- **Where:** The message was addressed to `hr@inergy.com` and was detected by the `SERVER-MAIL` alert.
- **Why:** The likely objective was to trick an HR employee into opening a malicious attachment by disguising it as a job application. The sender identity and message content are suspicious.

## Reasons for escalation

1. **Confirmed malicious indicator:** The SHA-256 hash of `bfsvc.exe` matches the known malicious file hash supplied in the alert.
2. **Suspicious sender and message:** The sender's unusual domain does not clearly correspond to the claimed identity, and the email contains spelling and grammar errors (including the misspelled job title and company name).
3. **Potential malware execution:** The alert says the user may have opened the email, attachment, or links. This is not proof that the executable ran, so endpoint investigation is required.

## Ticket comments

Investigated phishing alert A-2703 involving a suspicious email sent to hr@inergy.com by a sender claiming to be Clyde West on July 20, 2022. The email contained a password-protected executable attachment named bfsvc.exe, which was confirmed malicious based on its SHA-256 hash (54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b).

The ticket is escalated because the attachment hash is confirmed malicious, the sender domain and message content are suspicious, and the password-protected executable was disguised as a resume. Further investigation is needed to determine whether the recipient opened the attachment, whether the file executed, and whether the endpoint was compromised.

## Recommended next steps for the escalated team

- Confirm whether the recipient opened the email or extracted/opened the attachment.
- Review endpoint telemetry, process execution, file activity, persistence mechanisms, and network connections around the relevant time.
- Determine whether the device requires containment or isolation, following the organization's incident response procedures.
- Search mailboxes and mail logs for other recipients or copies of the message; remove or quarantine the email and attachment where appropriate.
- Preserve relevant email, endpoint, and network evidence for the investigation.

## Analyst notes and limitations

- The malicious hash is confirmed by the scenario.
- The alert does **not** establish that the attachment was executed or that the endpoint was compromised.
- The sender's identity and intent have not been independently verified.
- The email's displayed date is from 2022; use the organization's available logs and retention sources to determine what evidence remains.

**Disposition: Escalation.**