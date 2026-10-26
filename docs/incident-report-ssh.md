# Incident Report: Repeated SSH Authentication Failures

## 1. Incident Summary

| Field | Details |
|---|---|
| Incident type | Repeated SSH authentication failures |
| Environment | Controlled Wazuh SOC lab |
| Monitored endpoint | `ubuntu-endpoint-01` |
| Detection rule | Custom rule `100100` |
| Alert severity | Level 10 |
| Detection threshold | Five matching events within 120 seconds |
| MITRE ATT&CK | T1110.001 — Password Guessing |
| Validation status | Detection verified in the lab |

## 2. Objective

Validate whether a custom Wazuh correlation rule can identify repeated SSH authentication failures associated with the same source IP within a defined time window.

## 3. Detection Logic

The custom rule correlates events matching rule ID `5710`. It requires five matching events within 120 seconds and applies a same-source-IP condition.

```xml
<rule id="100100" level="10" frequency="5" timeframe="120">
  <if_matched_sid>5710</if_matched_sid>
  <same_srcip />
  <description>SSH: Repeated nonexistent-user login attempts from the same source IP within 120 seconds</description>
  <group>sshd,authentication_failed,invalid_login,</group>
  <mitre>
    <id>T1110.001</id>
  </mitre>
</rule>
```

This is the rule used in the lab. Preserve the installed configuration and validate the complete rule in the deployed Wazuh version before reusing it elsewhere.

## 4. Observed Evidence

During controlled validation, the rule triggered in Wazuh Dashboard.

- Rule ID: `100100`
- Level: `10`
- Description: Repeated nonexistent-user login attempts from the same source IP within 120 seconds
- Test username: `invalid_soc_user`
- Observed source IP: `127.0.0.1`

The event was generated in a local lab-testing context. It should not be represented as an attack originating from an external host.

Attach the original dashboard screenshot to the repository's evidence or screenshots folder and link it here after uploading.

## 5. Analyst Triage Procedure

1. Confirm the alert's rule ID, timestamp, endpoint, source IP, and event description.
2. Review the related authentication failures around the alert timestamp.
3. Determine whether the source is local, a known administrative host, or an unexpected remote system.
4. Check the targeted username and whether any subsequent successful authentication occurred.
5. Review surrounding SSH and system logs for relevant activity.
6. Determine whether the activity is an authorized test, operational error, or suspicious behavior.
7. Document the evidence, assessment, and next steps.

## 6. Recommended Response

For a real environment, follow the organization's incident-response policy.

- Preserve relevant logs and alert details.
- Validate the source host and account context.
- Investigate related successful logins and other suspicious activity.
- If malicious activity is supported by evidence, escalate and apply approved containment measures.
- Tune the rule if legitimate activity repeatedly causes false positives.

Do not block an address or disable an account solely because this lab rule triggered.

## 7. Conclusion

The custom correlation rule successfully generated a Level 10 Wazuh alert during controlled testing. This validates the configured detection path for the tested scenario. It does not, by itself, prove a successful brute-force attack or account compromise.

## 8. Evidence

Add the actual dashboard screenshot showing rule `100100` here once it is committed to the repository.
