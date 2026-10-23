# Detection Rules

Store custom Wazuh rules and their test notes here.

At present, no custom rule is claimed as implemented. First inspect the actual SSH event and determine whether an existing built-in rule meets the objective.

When adding a custom rule, include:
- The rule file or relevant XML snippet
- The detection objective and expected behavior
- A positive test case
- A negative test case
- The resulting alert fields and severity
- Any ATT&CK mapping, only if justified and verified

Never copy a rule into production systems without reviewing the effects and testing it in the lab.
