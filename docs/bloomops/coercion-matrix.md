# BloomOps Coercion Matrix

This matrix defines allowed verb downgrades or splits and explicitly disallowed transitions.
Use it only when strict-mode validation fails or a requested verb is too ambitious for the available inputs.

## Allowed coercions

| Requested Verb | Coerced Verb | Rule Type | Rationale | When to Apply |
| --- | --- | --- | --- | --- |
| CREATE | UNDERSTAND | Downgrade | Missing creative requirements; focus on comprehension of inputs. | User provides only background material without design goals. |
| CREATE | APPLY | Downgrade | Inputs define procedures; execution is needed rather than invention. | User supplies a fixed process or rubric to follow. |
| EVALUATE | ANALYZE | Downgrade | Criteria are absent; analysis can still surface parts and patterns. | User asks for judgment without providing criteria. |
| ANALYZE | UNDERSTAND | Downgrade | Not enough structure to decompose; can restate meaning. | Inputs are short or purely descriptive. |
| APPLY + EVALUATE | APPLY then EVALUATE | Split | Execution needs to happen before judgment. | Output depends on computed result and then a verdict. |
| ANALYZE + EVALUATE | ANALYZE then EVALUATE | Split | Evaluation must cite analysis evidence. | User requests both decomposition and judgment with clear criteria. |
| UNDERSTAND + APPLY | UNDERSTAND then APPLY | Split | Clarify meaning before running procedures. | Inputs are ambiguous but include a defined method. |

## Disallowed coercions

| Requested Verb | Disallowed Transition | Reason |
| --- | --- | --- |
| UNDERSTAND | CREATE | Upgrading invents new material beyond inputs. |
| REMEMBER | ANALYZE/EVALUATE | Memory recall cannot be turned into judgment or decomposition without new instruction. |
| APPLY | CREATE | Application cannot become invention without explicit design intent. |
| EVALUATE | CREATE | Judging is not a license to author new artifacts. |
| ANY | RANDOM/NON-VERB | Unsupported action, must fail strict mode. |

## Enforcement notes

- Coercion is **opt-in** only when strict mode would otherwise block execution.
- All coercions must be logged and justified using the table above.
- If no allowed coercion applies, the system must return an invalid-verb error response.
