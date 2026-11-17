# Design History File (DHF)

**IBEHS 5P06 Capstone Project**

## Purpose

This Design History File is the authoritative record of our engineering design process. It allows an informed reader to understand how the project evolved, why decisions were made, and how the current design could be reproduced or continued.

## How to Use This DHF

1. Start with `00_Admin/Project_Plan/Gantt_Chart.md` for project status
2. Check `08_Design_Reviews/` for the latest discussion document
3. Use `09_Decisions_Log/` to trace important decisions to their evidence

## Folder Structure

<!-- FOLDER_TABLE_START -->
| Folder | Contents |
|--------|----------|
| `.agents/` | Project documentation and files |
| `.claude/` | Project documentation and files |
| `00_Admin/` | Team roles, responsibilities, Gantt chart, project plan |
| `01_Background/` | Literature reviews, stakeholder communications, standards & regulations |
| `02_Meetings/` | Meeting agendas, minutes, action items |
| `03_Design/` | Concept generation, evaluation matrices, detailed design |
| `04_Deliverables/` | Project documentation and files |
<!-- FOLDER_TABLE_END -->

## What's in Each Folder

- **`00_Admin/`**: project management.
  - `Project_Plan/`: the fall work breakdown, with task IDs (F, D, L, T, G) and the milestone mapping.
  - `Stakeholder_Milestones/`: milestone plans as Markdown (`Markdown_Files/`) and the PDFs generated from them (`PDF_Outputs/`, built automatically, don't edit).
  - `Env_Testing/`: environment tests.
  - `ToolsInstallationGuide.md`: tools and packages to install.
- **`01_Background/`**: project facts and research.
  - `Established_Information/MasterDoc.md`: the authoritative record of confirmed project facts. Read this first.
  - `Literature_Review/`: background research.
- **`02_Meetings/`**: meeting notes, using `MTG-Template.md`.
  - `Instructor_Meetings/`, `Stakeholder_Meetings/`, `Weekly_Meetings/`, `Internal_Meetings/`.
- **`03_Design/`**: design work.
  - `01_Concept_Generation/`: brainstorming and milestone planning.
  - `02_Design_Decisions/`: design decisions and their reasoning; `01_Throwaway_Tests/` summarizes the throwaway tests.
- **`04_Deliverables/`**: course submissions (team charter, approval form, progress reports).
- **`scripts/`**: helper scripts used by the GitHub Actions (e.g. updating the folder table above).
- **`.agents/`, `.claude/`**: instructions for AI assistants working in this repo.

## Related Repositories

- [**Capstone-Throwaway-Tests**](https://github.com/KUBS-Engineering-Inc/Capstone-Throwaway-Tests): the throwaway test code. One module per test (frame extraction, window segmentation, scale OCR, Doppler waveform, ECG, perpendicular diameter, circular vessel detection), each with a README covering how to run it, what it does and its design decisions, plus a test harness that runs the modules as a pipeline and compares runs.

## File Naming Convention

Use the format: `YYYY-MM-DD_Description.md`

Examples:
- `2026-09-15_Meeting_Minutes.md`
- `DEC-001_Concept_Selection.md`
- `TEST-001_Initial_Test_Procedure.md`

## Revision History

| Date | Version | Changes |
|------|---------|---------|
| 2026-09-14 | 1.0 | Initial DHF structure created |
| 2026-11-16 | 1.1 | Added folder contents and related repositories sections |
