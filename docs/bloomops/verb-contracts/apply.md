# Verb Contract: APPLY

## Purpose
Use provided rules or procedures to produce a result from specified inputs.

## Required sections
- **Purpose**
- **Required Sections**
- **Forbidden Moves**
- **Valid Output Shape**
- **Strict-Mode Note**

## Forbidden moves
- Inventing rules or steps not in the inputs.
- Skipping required inputs or assuming defaults.
- Changing section titles or order.

## Valid output shape
```text
Purpose: <single sentence>
Inputs Used:
- <input name>: <value>
Steps:
1. <step 1>
2. <step 2>
Result:
- <output value>
```

## Strict-mode note
If any input is missing, any step is invented, or the format changes, strict mode must block execution.
