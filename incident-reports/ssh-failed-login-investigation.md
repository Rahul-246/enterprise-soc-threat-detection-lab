# SSH Failed-Login Detection — Lab Investigation

## 1. Summary

**Status:** Initial event visibility confirmed; detailed alert classification pending verification.

This investigation documents a controlled SSH failed-login simulation on a lab endpoint and the corresponding event observed in Wazuh Threat Hunting.

## 2. Environment

- **SIEM:** Wazuh
- **Endpoint agent:** `ubuntu-endpoint-01`
- **Test location:** SSH to localhost on the lab endpoint
- **Test account name:** `invalid_soc_user`
- **Test type:** Controlled lab simulation

## 3. Objective

Confirm that SSH authentication events are generated on the endpoint, collected by Wazuh, and available for investigation in Threat Hunting.

## 4. Verification results

| Check | Result |
|---|---|
| Wazuh Manager service | Passed — reported active |
| Wazuh Indexer service | Passed — reported active |
| Wazuh Dashboard service | Passed — dashboard accessible |
| Wazuh Agent service | Passed — reported running |
| Agent registration | Passed — `ubuntu-endpoint-01` reported Active |
| SSH test event visibility | Passed — event reported visible in Threat Hunting |

## 5. Event details — fill from the actual event

- **Event timestamp:** TODO
- **Agent ID:** TODO
- **Agent name:** `ubuntu-endpoint-01`
- **Rule ID:** TODO
- **Rule description:** TODO
- **Rule level / severity:** TODO
- **Rule groups:** TODO
- **Source IP (if present):** TODO
- **Username field (if present):** TODO
- **MITRE ATT&CK technique (only if present in rule metadata):** TODO

Do not guess or fabricate event metadata. If a field is absent, write “Not present in this event.”

## 6. Analysis

The test was intentionally performed against localhost on a lab endpoint. This creates local authentication-failure activity; it does not represent an external attacker. The source address may therefore be loopback (`127.0.0.1` or `::1`) if recorded.

Confirm whether the event is a raw/decoded event, a generated alert, or both. Record only the classification supported by the Wazuh event details.

## 7. Evidence

Add screenshots in `../screenshots/`:

- `01-wazuh-dashboard.png`
- `02-wazuh-services.png`
- `03-agent-connected.png`
- `04-ssh-detection.png`

## 8. Outcome and next steps

- Confirm event timestamp and endpoint identity.
- Record exact rule metadata and severity.
- Verify any ATT&CK mapping from the rule metadata.
- If necessary, build a custom rule and test positive and negative cases.
- Document remediation and limitations after the detection behavior is validated.

**Disclosure:** This is a controlled lab simulation for educational purposes, not a report of a real-world compromise.
