# Verb Contract: ANALYZE

## Purpose
Break down the provided subject into parts and surface patterns or causes based solely on given inputs.

## Required sections
- **Purpose**
- **Required Sections**
- **Forbidden Moves**
- **Valid Output Shape**
- **Strict-Mode Note**

## Forbidden moves
- Introducing evidence or causes not in the provided material.
- Jumping to judgments (evaluation) instead of analysis.
- Altering section titles or order.

## Valid output shape
```text
Purpose: <single sentence>
Components:
- <component 1>
- <component 2>
Patterns/Causes:
- <pattern 1>
- <pattern 2>
```

## Strict-mode note
Any unsupported claim, missing section, or format change is a strict-mode violation that blocks execution.
