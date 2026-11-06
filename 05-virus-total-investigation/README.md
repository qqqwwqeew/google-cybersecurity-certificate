# VirusTotal Malware Investigation

**Track:** Google Cybersecurity Certificate  
**Phase:** Detection and Analysis  
**Scenario:** Suspicious password-protected email attachment  
**Tools:** VirusTotal, threat-intelligence references  
**Status:** Completed as a simulated training investigation

## 1. Incident summary

A financial-services employee received an email with a password-protected spreadsheet attachment. The password was included in the email. After the employee downloaded and opened the attachment, unauthorized executable files appeared on the workstation and an intrusion-detection alert was sent to the SOC.

The investigation starts from the file's SHA-256 hash and uses threat-intelligence data to identify related indicators of compromise (IoCs).

### Event timeline

| Time | Event |
|---|---|
| 13:11 | Employee receives an email with an attachment |
| 13:13 | Employee downloads and opens the password-protected file |
| 13:15 | Multiple unauthorized executable files are created |
| 13:20 | IDS detects the executables and alerts the SOC |

## 2. Initial file indicator

| Field | Value |
|---|---|
| SHA-256 | `54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b` |
| SHA-1 | `8f35a9e70dbec8f1904991773f394cd4f9a07f5e` |
| MD5 | `287d612e29b71c90aa54947313810a25` |
| Reported filename in a public sample record | `54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b.bin` |

The SHA-1 and MD5 values are additional hashes associated with the same SHA-256 sample in MalwareBazaar's record.

## 3. Verdict

**Assessment: Malicious.**

The course exercise's VirusTotal lookup reports that 58 of 72 security vendors detected the sample. Multiple public threat-intelligence records also classify the sample as malicious and associate it with Flagpro / BlackTech.

A high detection ratio across multiple vendors, together with independent malware-intelligence records, supports treating the file as malicious. Vendor results can change over time, and no single scanner is conclusive.

> Note: 58/72 is the reported vendor detection ratio. It is not a VirusTotal community score.

## 4. Three indicators of compromise

The following three IoC types were selected for the exercise. Network indicators are defanged below to reduce the chance of accidental navigation.

| Pyramid of Pain category | Indicator | How it can be used |
|---|---|---|
| Hash value (SHA-1) | `8f35a9e70dbec8f1904991773f394cd4f9a07f5e` | Search for or detect the exact file sample |
| Domain name | `org[.]misecure[.]com` | Search DNS, proxy, firewall and endpoint telemetry for connections to the domain |
| IP address | `139[.]162[.]87[.]180` | Search network logs and relevant controls for connections to the IP |

**Validation note:** The SHA-1 is listed alongside the sample in MalwareBazaar. The domain is identified as a malicious contacted domain in the course exercise reference. The IP appears in a public threat-intelligence IoC list associated with this sample. These are threat-intelligence leads; an analyst should verify each indicator against the current VirusTotal Relations / Behavior data and the organization's own telemetry before blocking it.

## 5. Pyramid of Pain interpretation

This investigation uses three of the six indicator categories:

- **Hash values:** generally easy for an attacker to change by modifying or rebuilding a file.
- **IP addresses:** can be changed by moving infrastructure or using different hosts.
- **Domain names:** can be replaced by registering or compromising other domains.

These indicators are useful for detection and threat hunting, but they are generally lower on the Pyramid of Pain than tools, network/host artifacts, and attacker tactics, techniques, and procedures (TTPs). Blocking one indicator may disrupt a campaign temporarily without stopping the actor.

## 6. Suggested SOC response

1. Isolate the affected workstation from the network while preserving evidence.
2. Escalate the confirmed malicious attachment to the incident-response team.
3. Preserve the original email, attachment, relevant endpoint telemetry and timestamps.
4. Search endpoint, DNS, proxy and firewall logs for the listed indicators.
5. Identify and investigate any additional executables or persistence mechanisms created after execution.
6. Remove the malware and restore the workstation according to the organization's incident-response process.
7. Hunt for the same indicators across other endpoints and mailboxes.
8. Treat the listed domain and IP as leads and validate them before deploying blocks.

## 7. Limitations

This is a simulated course scenario documented using public threat-intelligence references. It does not include access to the organization's endpoint logs, the original email, or a live forensic image. No claim is made that the listed network indicators were observed in the fictional organization's environment.

The vendor detection ratio is time-sensitive and may differ when the VirusTotal report is viewed later. This repository does not contain the malware sample.

## 8. References

- [VirusTotal report for the SHA-256](https://www.virustotal.com/gui/file/54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b)
- [MalwareBazaar sample record](https://bazaar.abuse.ch/sample/54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b/)
- [Course exercise reference and VirusTotal findings](https://www.danieldurgaprasad.com/detection-and-response)
- [Public threat-intelligence IoC reference](https://static.claro.com.pe/img/otros/Boletin_Ciberseguridad_Enero_S2.pdf)

---

*Educational lab documentation. Do not treat this report as a production incident assessment or use an indicator for blocking without local validation.*
