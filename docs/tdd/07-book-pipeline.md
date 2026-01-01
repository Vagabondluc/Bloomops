# TDD 07: Book Pipeline Artifacts

## Coverage
- TDD-090, TDD-091, TDD-092, TDD-093, TDD-094, TDD-095, TDD-096, TDD-097

## Artifact Outputs

ID: TDD-090  
Global artifacts are created at expected paths (callsheet, characters, worldbuilding, outline, style sheet).

ID: TDD-091  
Per-scene artifacts are created at expected paths for each scene.

ID: TDD-092  
`compile-chapter` creates `chapter.md` by concatenating scenes in order.

ID: TDD-093  
`append-chapter` adds `chapter.md` to `manuscript.md` in outline order.

ID: TDD-094  
Each node emits a checksum and summary in outputs.

ID: TDD-095  
Word count, POV, and prohibited word checks are recorded for each scene.

ID: TDD-096  
A completed manuscript includes all chapters and all scenes with no duplicates.

ID: TDD-097  
Given an invalidated scene, the pipeline regenerates a versioned scene and recompiles the chapter with the latest valid scene.

## QA Checklist
Inputs:
- Completed run outputs
Steps:
1. Verify artifact paths, checksums, and scene checks.
Expected:
- All artifacts exist, checksums recorded.
- Manuscript contains all scenes/chapters without duplicates.
