# Verb Contract: REMEMBER

## Purpose
Capture and restate previously provided facts or definitions without adding new information.

## Required sections
- **Purpose**
- **Forbidden Moves**
- **Valid Output Shape**
- **Strict-Mode Note**

## Forbidden moves
- Introducing facts not explicitly in the provided memory sources.
- Reframing or paraphrasing in a way that changes meaning.
- Omitting any required section or changing its heading.

## Valid output shape
```text
Purpose: <single sentence>
Facts:
- <fact 1>
- <fact 2>
Constraints:
- <constraint 1>
- <constraint 2>
```

## Strict-mode note
Any missing section, added information, or altered headings is a strict-mode violation and must block execution.
