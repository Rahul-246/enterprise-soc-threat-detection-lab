# Enterprise SOC Lab: Threat Detection & Incident Response

A hands-on home lab built with Wazuh to practice endpoint monitoring, security-event investigation, and incident documentation.

> **Status:** Initial lab validation completed by the author. Add your own screenshots and exact event metadata before publishing.
> **Environment:** VMware Workstation, Ubuntu Server 24.04 LTS, Wazuh all-in-one server, Ubuntu endpoint with Wazuh Agent.

## Objectives

- Deploy a Wazuh Manager, Indexer, and Dashboard.
- Enroll a Linux endpoint with the Wazuh Agent.
- Generate controlled SSH authentication failures on a system owned by the lab operator.
- Verify event visibility and investigate the corresponding Wazuh event.
- Document evidence, findings, limitations, and defensive recommendations.

## Architecture

See [`architecture/lab-architecture.md`](architecture/lab-architecture.md).

## Lab components

| Component | Role |
|---|---|
| VM1 — Wazuh Server | Manager, Indexer, Dashboard |
| VM2 — Ubuntu Endpoint | Wazuh Agent and local authentication logs |
| Windows host | Browser-based dashboard access, screenshots, documentation |

## Validation status

The following checks were reported as passing during lab setup:

- Wazuh Manager, Indexer, and Dashboard services active.
- Wazuh Agent service running on the endpoint.
- Agent `ubuntu-endpoint-01` shown as Active in the dashboard.
- SSH test event visible in Wazuh Threat Hunting.

Before publishing, attach your own screenshots and replace placeholders in the investigation report with the exact values from the event details.

## Repository structure

```text
.
├── README.md
├── architecture/
│   └── lab-architecture.md
├── detection-rules/
│   └── README.md
├── incident-reports/
│   └── ssh-failed-login-investigation.md
└── screenshots/
    └── README.md
```

## Evidence checklist

- [ ] `01-wazuh-dashboard.png`
- [ ] `02-wazuh-services.png`
- [ ] `03-agent-connected.png`
- [ ] `04-ssh-detection.png`
- [ ] Exact event timestamp, rule ID, rule description, severity, and source IP (if present)
- [ ] Detection behavior validated with repeatable test events

## Safety and privacy

- Only test against systems you own or are explicitly authorized to assess.
- This repository documents a controlled lab simulation, not a real-world intrusion.
- Never commit passwords, tokens, private keys, enrollment credentials, or sensitive logs.
- Review screenshots for secrets, personal information, and unnecessary network details before publishing.
- Do not claim custom detection engineering or MITRE ATT&CK mapping unless you have implemented and verified it.

## Next improvements

1. Add event screenshots and exact metadata.
2. Verify the relevant rule and event classification.
3. Develop a custom detection rule only if the existing detection does not meet the lab objective.
4. Test the rule against positive and negative cases.
5. Add a repeatable test procedure and lessons learned.
