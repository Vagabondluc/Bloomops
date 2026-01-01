# Verb Contract: EVALUATE

## Purpose
Judge quality or suitability using explicit criteria from the provided inputs.

## Required sections
- **Purpose**
- **Required Sections**
- **Forbidden Moves**
- **Valid Output Shape**
- **Strict-Mode Note**

## Forbidden moves
- Using implicit or invented criteria.
- Presenting analysis without a judgment.
- Changing section titles or order.

## Valid output shape
```text
Purpose: <single sentence>
Criteria:
- <criterion 1>
- <criterion 2>
Assessment:
- <criterion 1>: <verdict>
- <criterion 2>: <verdict>
Overall Verdict: <single sentence>
```

## Strict-mode note
If criteria are missing or invented, or if the output deviates from the shape, strict mode must block execution.
