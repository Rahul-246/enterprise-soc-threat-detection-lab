# Wazuh SOC Lab — Detection Validation Matrix

## 1. Purpose

This matrix records the detection scenarios tested in the Wazuh SOC lab, the expected outcomes, and the observed results.

The results reflect controlled lab validation, not a claim of comprehensive security coverage.

## 2. Environment

- SIEM: Wazuh
- Wazuh version observed during testing: `4.14.9`
- Manager host: `u1`
- Monitored endpoint: `ubuntu-endpoint-01` (`u2`)
- FIM test directory: `/var/ossec/fim-test`

## 3. Test Results

| Test ID | Scenario | Expected result | Observed result | Status |
|---|---|---|---|---|
| SSH-01 | Repeated matching SSH authentication failures from the same source IP | Custom rule `100100` generates a Level 10 alert after the configured threshold | Rule `100100` triggered during controlled testing | PASS |
| FIM-01 | Modify a file in the monitored test directory | Rule `550` reports a checksum change | Level 7 alert observed | PASS |
| FIM-02 | Delete a file in the monitored test directory | Rule `553` reports file deletion | Level 7 alert observed | PASS |
| SYS-01 | Check Wazuh manager service | Service reports active | Active when checked | PASS |
| SYS-02 | Check Wazuh indexer service | Service reports active | Active when checked | PASS |
| SYS-03 | Check Wazuh dashboard service | Service reports active | Active when checked | PASS |

## 4. SSH Correlation Rule

| Property | Value |
|---|---|
| Custom rule ID | `100100` |
| Severity level | `10` |
| Frequency | `5` |
| Timeframe | `120` seconds |
| Parent rule | `5710` |
| Correlation condition | Same source IP |
| MITRE ATT&CK | `T1110.001` — Password Guessing |

The custom rule was tested using repeated matching authentication-failure events. The rule triggered in the Wazuh log test and a corresponding alert was later observed in the dashboard.

**Context:** The observed source IP was `127.0.0.1`, and the test username was `invalid_soc_user`. This was a controlled local simulation, not evidence of an external attacker.

## 5. File Integrity Monitoring

| Property | Value |
|---|---|
| Monitored directory | `/var/ossec/fim-test` |
| Monitoring configuration | `check_all="yes"` and `realtime="yes"` |
| Modification rule | `550` |
| Deletion rule | `553` |
| Observed alert level | `7` for both alerts |

The modification and deletion tests generated the expected alerts in the dashboard.

## 6. Evidence Checklist

Add links to actual screenshots in the repository after confirming their committed paths.

- [ ] Dashboard alert for custom SSH rule `100100`
- [ ] Dashboard alert for FIM modification rule `550`
- [ ] Dashboard alert for FIM deletion rule `553`
- [ ] Service-health checks showing manager, indexer, and dashboard active
- [ ] Optional screenshot of the relevant custom rule configuration

Do not mark an evidence item complete until the corresponding screenshot is committed and its path has been verified.

## 7. Limitations

- The tests cover three detection outcomes and basic service-health checks.
- They do not establish comprehensive detection coverage or absence of false negatives.
- The SSH test does not demonstrate a successful compromise.
- No automated blocking, containment, or remediation was validated.
- Service health reflects the time at which the checks were performed.

## 8. Conclusion

The lab successfully validated the custom SSH correlation rule, file modification detection, and file deletion detection. These results provide evidence of practical Wazuh configuration, detection validation, and introductory SOC triage skills.
