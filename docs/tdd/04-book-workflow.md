# TDD 04: Book Workflow

## Coverage
- TDD-040, TDD-041, TDD-041a, TDD-042, TDD-042a, TDD-043
- TDD-044, TDD-044a, TDD-045, TDD-045a, TDD-045b
- TDD-046, TDD-047, TDD-048, TDD-048a, TDD-049, TDD-049a
- TDD-049b, TDD-049c, TDD-049d, TDD-049e
- TDD-060, TDD-061, TDD-062, TDD-063, TDD-064

## Workflow Outputs

ID: TDD-040  
Given `book/Jason's Prompts.md`, the system maps each step to Bloom verbs as specified in `docs/specs/04-book-workflow.md`.

ID: TDD-041  
Given the call sheet prompt inputs, the output matches the required Markdown format.

ID: TDD-041a  
Call sheet output includes character, worldbuilding, and outline sections in order.

ID: TDD-042  
Given character and worldbuilding inputs, the outline output includes chapter summaries with 200-250 words each.

ID: TDD-042a  
Outline output uses the required Markdown headings for each chapter.

ID: TDD-043  
Given style sheet inputs, the output includes all required sections and example snippets.

ID: TDD-044  
Given scene brief inputs, the output includes all required fields (POV, beats, setting, conflict, continuity).

ID: TDD-044a  
Scene brief includes the exact chapter label and verbatim plot summary.

ID: TDD-045  
Given scene draft inputs, the output respects prohibited words, POV, and word-count constraints.

ID: TDD-045a  
Scene draft includes markdown heading for the scene and does not alter scene order.

ID: TDD-045b  
Scene draft uses previous scene text as continuity input.

ID: TDD-046  
Given an improvement plan prompt, the output includes a clear, ordered edit plan referencing the scene brief.

ID: TDD-047  
Given an improvement plan and draft, the edit pass updates only the specified issues and preserves scene structure.

ID: TDD-048  
Given a revised scene, the copyproof pass removes grammar errors and AI-isms without changing plot events.

ID: TDD-048a  
Copyproof output preserves headings and scene boundaries.

ID: TDD-049  
Given a copyproofed scene, tighten pass 1 reduces wordiness while preserving meaning.

ID: TDD-049a  
Given a tighten pass 1 output, tighten pass 2 applies a final polish without reintroducing prohibited words.

ID: TDD-049b  
Given scene outputs, append-scene adds content to the chapter once per scene ID and preserves order.

ID: TDD-049c  
Given scene outputs for a chapter, compile-chapter concatenates scenes in order and produces `chapter.md`.

ID: TDD-049d  
Given chapter outputs, append-chapter adds content to the manuscript once per chapter ID and preserves order.

ID: TDD-049e  
Given scene outputs, compile-chapter preserves scene order and boundaries.

## End-to-End QA Checklists

### TDD-060: Minimal Pipeline Smoke Test
Inputs:
- BloomOps Markdown with `scene_plan` for 1 chapter, 1 scene
- JSON/YAML with `doctrine_frozen: true`
Steps:
1. Run outline generation.
2. Run scene brief -> draft -> critique -> apply edits.
3. Verify artifacts and logs after each node.
Expected:
- All nodes succeed and emit logs.
- Artifacts exist for outline, scene brief, draft, improvement plan, revised output.

### TDD-061: Failure Halt Test
Inputs:
- Same as TDD-060, but with one missing required input
Steps:
1. Run the pipeline until the missing-input node.
Expected:
- Pipeline halts on failure.
- Last successful artifact is reported.
- Failure summary includes error details.

### TDD-062: Two-Scene Continuity Test
Inputs:
- BloomOps `scene_plan` with two scenes in one chapter
- JSON/YAML frozen
Steps:
1. Run scene loop for both scenes.
2. Inspect scene 2 inputs for previous scene text.
Expected:
- Scene 2 receives previous scene text.
- Scene append preserves order.

### TDD-063: Two-Chapter Continuity Test
Inputs:
- BloomOps `scene_plan` with two chapters (1 scene each)
- JSON/YAML frozen
Steps:
1. Run pipeline through chapter 1 completion.
2. Start chapter 2 and inspect first scene inputs.
Expected:
- Chapter 2 scene 1 receives previous chapter text.
- Manuscript includes chapter 1 before chapter 2.

### TDD-064: One-Chapter Two-Scene Manuscript Test
Inputs:
- BloomOps `scene_plan` with one chapter, two scenes
- JSON/YAML frozen
Steps:
1. Run full scene loop.
2. Compile chapter.
3. Append chapter to manuscript.
Expected:
- `chapter.md` includes both scenes in order.
- `manuscript.md` includes the compiled chapter once.
