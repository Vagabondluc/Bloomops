# Invalid/Unknown Verb Policy

## Detection
- Compare requested verb against the approved BloomOps verb list.
- Reject if the verb is missing, misspelled, or not mapped to a strict-mode contract.
- Reject if a verb is present but required fields in its contract are incomplete.

## Error output format
```text
Error: INVALID_VERB
Requested: <original verb>
Reason: <unknown verb | missing contract | malformed contract>
Allowed Verbs: <comma-separated list>
Next Step: <remediation step>
```

## Remediation steps
- Ask the user to restate the request with an allowed verb.
- Suggest the nearest valid verb based on intent and inputs.
- Offer a coercion only when permitted by the coercion matrix.
- If no remediation is possible, halt automation and request clarification.

## Strict-mode enforcement
Any invalid or unknown verb must terminate execution and return the error output format above.
