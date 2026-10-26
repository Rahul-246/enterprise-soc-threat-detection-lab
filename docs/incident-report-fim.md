# Incident Report: File Integrity Monitoring

## 1. Incident Summary

| Field | Details |
|---|---|
| Incident type | File modification and deletion |
| Monitored endpoint | Ubuntu endpoint `u2` |
| Monitored directory | `/var/ossec/fim-test` |
| Modification rule | `550` |
| Deletion rule | `553` |
| Alert level | `7` for both observed alerts |
| Validation status | Both tests verified in the lab |

## 2. Objective

Validate that Wazuh File Integrity Monitoring (FIM) detects changes to files in a designated test directory and generates alerts that can be reviewed by a SOC analyst.

## 3. Configuration

The endpoint's Wazuh agent configuration includes the following directory entry inside the `syscheck` configuration:

```xml
<directories check_all="yes" realtime="yes">/var/ossec/fim-test</directories>
```

The `syscheck` component was enabled. The test directory was created, a test file was written, and the Wazuh agent was restarted after the configuration change.

## 4. Test Procedure and Results

### Test A: File Modification

1. Create a test file in `/var/ossec/fim-test`.
2. Modify the file's contents.
3. Review the Wazuh Dashboard for the resulting alert.
4. Confirm the rule ID and event description.

**Observed result:** Wazuh generated rule `550`, Level 7, with the description `Integrity checksum changed`.

**Assessment:** The monitored file modification was detected.

### Test B: File Deletion

1. Delete the test file from `/var/ossec/fim-test`.
2. Review the Wazuh Dashboard for the resulting alert.
3. Confirm the rule ID and event description.

**Observed result:** Wazuh generated rule `553`, Level 7, with the description `File deleted`.

**Assessment:** The monitored file deletion was detected.

## 5. Analyst Investigation Workflow

For an unexpected file change, the analyst should:

1. Identify the affected endpoint, file path, event timestamp, and rule ID.
2. Determine whether the change was authorized.
3. Identify the relevant user, process, or maintenance activity where logs provide that information.
4. Compare the event with approved software changes, system updates, or administrative tasks.
5. Investigate related alerts and authentication activity.
6. Preserve relevant evidence and record the investigation findings.
7. Escalate suspicious or unauthorized changes according to organizational policy.

A FIM alert indicates a detected filesystem change; it does not automatically prove malicious activity.

## 6. Recommended Response

For a production incident, validate the file's purpose and the change's authorization before acting. Preserve evidence, consult approved baselines or backups, and escalate potentially malicious changes. Restore files only through an authorized recovery process.

## 7. Conclusion

Both controlled FIM tests generated the expected Wazuh alerts: rule `550` for modification and rule `553` for deletion. These results demonstrate successful validation of the tested file-monitoring scenarios.

## 8. Evidence

Add the actual dashboard screenshots showing the modification and deletion alerts to the repository's existing evidence or screenshots folder. Link the committed images here once their paths are confirmed.
