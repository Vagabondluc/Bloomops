# BloomOps Documentation

## Constraints

**This does not make AI smarter.**

## BloomOps doctrine (strict mode)

- Verbs require explicit contracts, schemas, and validated inputs before execution.
- Outputs must match the declared output shape exactly; format drift is a failure.
- Forbidden moves block execution and trigger remediation or coercion checks.
- Coercions are allowed only per the coercion matrix and must be logged with rationale.
- Invalid or unknown verbs halt automation and return a structured error response.
