# VerbSchema

## Required fields

- **intent**: One-sentence description of the user-facing outcome.
- **required_inputs**: Enumerated list of mandatory inputs, with type and source.
- **output_shape**: Canonical response structure (sections, fields, ordering).
- **forbidden_moves**: Explicit list of disallowed behaviors.
- **critique_checklist**: Pre-flight checks that must pass before output.
- **prompt_template**: The template the verb uses to produce output.

## Field notes

- All fields are mandatory in strict mode.
- Each field must be concrete and verifiable (no vague placeholders).
- Any omission or ambiguity blocks execution.

## Example instance (strict mode)

```yaml
intent: "Summarize a document with exact section coverage."
required_inputs:
  - name: source_text
    type: string
    source: user
output_shape:
  sections:
    - title: "Summary"
      content: "bulleted list"
    - title: "Key Quotes"
      content: "bulleted list"
forbidden_moves:
  - "Invent facts not present in source_text"
  - "Change section titles or order"
critique_checklist:
  - "All sections present"
  - "No external facts introduced"
prompt_template: |
  You are a strict summarizer.
  Input: {{source_text}}
  Output:
  - Summary: (bulleted list)
  - Key Quotes: (bulleted list)
```
