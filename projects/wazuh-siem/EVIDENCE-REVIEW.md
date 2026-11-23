# Wazuh SOC Lab — Evidence Intake and Publication Checklist

**Current status: reported available by project owner; original screenshots and log excerpts have not yet been inspected.** Do not mark items verified solely from their availability.

## Required evidence filenames (redacted copies only)

| ID | Suggested public file | Required verification | Publication state |
|---|---|---|---|
| E01 | `evidence/01-wazuh-services-redacted.png` | Manager, Indexer and Dashboard service names and `active (running)` states; capture timestamps or separate images where needed | Pending review |
| E02 | `evidence/02-wazuh-agents-redacted.png` | Both bastion and WAF agents active, correct host roles | Pending review |
| E03 | `evidence/03-aws-security-group-redacted.png` | Port/protocol/source plus association with intended subnet/instance; no insecure exposure | Pending review |
| E04 | `evidence/04-dashboard-authenticated-redacted.png` | Authenticated dashboard, not just login form | Pending review |
| E05 | `evidence/05-detection-alert-redacted.png` | Rule/event ID, agent, timestamp, event context; correlate with sanitized log excerpt | Pending review |

Some results may require more than one screenshot. Filenames are suggestions, not proof that a file exists.

## Review criteria

- **Service state:** Does the screenshot unambiguously show all three services or their separate systemctl results?
- **Agent health:** Is the time of capture clear, and are two distinct agents active?
- **Security groups:** Is access restricted to appropriate source hosts/security groups, rather than `0.0.0.0/0` for management endpoints?
- **Dashboard:** Does the screenshot show a successful authenticated Wazuh session?
- **SOC detection:** Can the exact test action, source, log record, alert and analyst interpretation be connected? Do not equate an active agent with verified alert generation.

## Redaction checklist

Before committing any screenshot, screenshot-derived PDF, or log:

- Remove AWS account IDs, access keys, private keys, passwords, tokens, cookies, session IDs, and certificate private material.
- Mask live public IPs, revealing hostnames, internal asset identifiers, unique user identifiers and email addresses where unnecessary.
- Strip real-person or customer information from logs; use synthetic details only if unmistakably labeled as examples.
- Confirm the screenshot reveals no open browser tabs or dashboards containing confidential information.
- Preserve security-relevant port numbers, protocols, service names, timestamps and alert rules when safe.
- Review image metadata and filenames.
- Obtain permission for shared group work, instructor material, or third-party copyrighted screenshots before publishing.

**Important:** Redaction must be applied to a copy of the image before upload. Deleting a secret in a later commit may not remove it from Git history.

## Suggested investigation report structure

1. **Context:** Authorized academic lab, affected host role, lab timestamp and timezone.
2. **Test action:** The harmless action performed to generate the event (only if actually recorded).
3. **Raw evidence:** Sanitized event/log excerpt including timestamp and origin.
4. **Detection:** Wazuh rule ID, level, description, agent and alert timestamp.
5. **Analyst triage:** True positive, false positive, inconclusive, or not established; explain why.
6. **Impact and scope:** Confirmed facts vs hypotheses.
7. **Response:** Actions actually performed, with suggestions clearly labeled if not executed.
8. **Limitations:** Missing logs, incomplete telemetry, timing uncertainty or unsupported conclusions.

## Evidence status vocabulary

- **Available:** Owner has the source image/log.
- **Reviewed:** Evidence has been inspected for content and basic consistency.
- **Verified:** A claim is directly supported by reviewed evidence.
- **Published:** A sanitized, authorized copy is in the public repository.

Keep the original evidence private and add only sanitized copies under `evidence/` after review.
