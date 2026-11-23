# AWS Offline Wazuh SIEM — SOC Monitoring Lab

> **Status: Documentation in progress.** This is an academic lab case study, not a production deployment or workplace SOC engagement. The lab guide has been reviewed; successful installation, agent enrollment, and alert detection are **not yet verified** against the student's own evidence.

## Executive summary

This project investigates the deployment and validation of an offline, single-node Wazuh Security Information and Event Management (SIEM) platform in an AWS screened subnet. The design separates an internet-connected bastion host from the private SIEM server. The intended outcome is a functioning Wazuh Manager, Indexer and Dashboard, with monitoring agents on the bastion and WAF hosts.

**Source basis:** *Module 6C Lab: Wazuh Offline SIEM Server Installation*, academic lab guide provided for coursework. The guide establishes objectives and expected tests—not proof that they were completed.

## Why this matters for SOC work

- **Log visibility:** Endpoint agents can forward security telemetry for centralized review.
- **Detection operations:** Analysts can use correlated alerts to prioritize investigation and identify events needing escalation.
- **Infrastructure security:** A private SIEM server and restricted management pathways reduce unnecessary exposure.
- **Operational verification:** An analyst must distinguish a running service from a complete and useful detection pipeline. Agent status alone does not prove that meaningful events are being collected, indexed, and alerted on.

## Target architecture (from lab guide)

```text
                Internet (package retrieval)
                           |
                    AWS Bastion Host
                    (bundle preparation)
                           |
                   SCP / restricted SSH
                           |
              AWS screened / private subnet
                           |
                  Offline Wazuh SIEM VM
              +--------------------------+
              |  Wazuh Manager           |
              |  Wazuh Indexer           |
              |  Wazuh Dashboard         |
              +--------------------------+
                        ^
                        | Agent telemetry (planned)
           +------------+-------------+
           |                          |
      Bastion agent               WAF host agent
```

This is a conceptual architecture derived from the assignment, **not** an audited representation of a completed AWS deployment. IPs, subnet IDs, instance sizing and routing are intentionally omitted until verified and sanitized.

## Lab workflow defined by the assignment

1. Prepare an offline installation bundle on the internet-connected bastion host.
2. Configure Wazuh node definitions using the offline server's private IP.
3. Generate installation certificates and download installation packages.
4. Check the private server's CPU, RAM, disk and time synchronization.
5. Review AWS security groups and transfer the bundle into the screened subnet using SCP.
6. Follow the guide's Ubuntu 24.04 compatibility procedure as applicable.
7. Install and validate the Manager, Indexer, and Dashboard.
8. Enroll the specified endpoint agents and verify that the dashboard is accessible.

**Caution:** The lab guide includes sample addresses and command formatting that require review before use. Treat it as the course-specific task sequence; do not blindly run copied commands or expose management/API ports to the internet.

## Evidence and verification matrix

| Requirement | Evidence to collect | Status |
|---|---|---|
| AWS network boundaries | Sanitized VPC/subnet topology and security group rules | Not yet reviewed |
| Offline media preparation | Downloaded bundle files, checksums if recorded | Not yet reviewed |
| Transfer to private host | Redacted SCP output and local file listing | Not yet reviewed |
| Wazuh Indexer | `sudo systemctl status wazuh-indexer` | Not yet reviewed |
| Wazuh Manager | `sudo systemctl status wazuh-manager` | Not yet reviewed |
| Wazuh Dashboard | `sudo systemctl status wazuh-dashboard` | Not yet reviewed |
| Bastion host agent | Wazuh agent listing showing active status | Not yet reviewed |
| WAF host agent | Wazuh agent listing showing active status | Not yet reviewed |
| Dashboard accessibility | Redacted dashboard login screenshot | Not yet reviewed |
| Event ingestion and detection | Timestamped test event, agent/source, rule/alert and analyst interpretation | Not yet reviewed |

The first nine items correspond to setup and validation targets in Module 6C. The final event-ingestion/detection item is a **recommended additional SOC portfolio test**; it is not stated as a completed Module 6C result.

## Verification commands (for evidence collection)

These are **checks to run on the appropriate lab host**, not outputs from a completed run.

```bash
# On the Wazuh server
sudo systemctl status wazuh-indexer --no-pager
sudo systemctl status wazuh-manager --no-pager
sudo systemctl status wazuh-dashboard --no-pager
df -h
free -h
timedatectl
```

For a SOC-focused project, also document one safely generated test event, its time, the agent, the resulting alert (or absence of one), how the event was triaged, and any gaps in detection. Do not fabricate attack activity or alerts.

## Findings, challenges, and lessons learned

**Pending evidence review.** Distinguish observed results from interpretation and from the installation guide's *expected* output. Include troubleshooting only for problems personally encountered and resolved.

## Scope and limitations

- Academic test network; not representative of a production security operations centre.
- Successful software installation would not, by itself, establish monitoring effectiveness.
- Evidence of detection coverage, alert fidelity, response playbooks, retention, and high availability is still required for stronger operational claims.

## Privacy and publishing safeguards

Never publish private keys, credentials, enrollment secrets, authentication tokens, public or private addresses that reveal active infrastructure, sensitive logs, unredacted console screenshots, or instructor-owned lab materials. Use original summaries and recreated diagrams. Credit collaborators appropriately.

## Next evidence needed

1. Sanitized screenshots of the three running services.
2. Sanitized dashboard screenshot showing the two agents and their statuses.
3. AWS security group screenshot with account IDs and addresses redacted.
4. Any genuine test event/alert logs, including whether an alert was actually generated.

*Project owner: Shehani Ranasinghe. Source: academic Module 6C Wazuh lab guide; practical results pending verification.*
