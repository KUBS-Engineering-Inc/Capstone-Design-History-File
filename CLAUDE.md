# CLAUDE.md

This repo is the Design History File (DHF) for a IBEHS 5P06 capstone project (Team 12): a GUI application that analyzes duplex Doppler ultrasound videos to extract vessel diameter, cross-sectional area (CSA), blood velocity and blood flow, and integrates with the PhysioMerge (PM) lab software. It contains documentation only, no application code.

## Role

Help the team write and maintain documentation: milestones, planning assets, meeting notes, design records. Take natural-language input and synthesize existing repo content into clear writing. Don't invent technical facts.

## Source of truth

- `01_Background/Established_Information/MasterDoc.md` is the authoritative record of confirmed project facts (scope, views, hardware, input data, PM integration, validation baseline). Read it first for any technical content.
- If a fact isn't in the master doc, say so and keep that section brief rather than filling it with assumptions or future plans worded as if decided. Flag gaps so the user can supply or confirm the information.
- Meeting notes in `02_Meetings/` are raw inputs. Don't promote anything from them into deliverables unless the user says to, because the master doc is meant to hold only what the team has established.
- `00_Admin/Project_Plan/2026-10-02_Fall_Work_Breakdown.md` defines task IDs (F1–F12, D, L, T, G) and the milestone mapping. Reference those IDs when a deliverable corresponds to one.

## Layout

| Folder | Contents |
| --- | --- |
| `00_Admin/` | Project plan, stakeholder milestones (`Stakeholder_Milestones/Markdown_Files/`), env tests |
| `01_Background/` | Master doc, literature review |
| `02_Meetings/` | Instructor, stakeholder, weekly and internal meeting notes; template in `MTG-Template.md` |
| `03_Design/` | Concept generation, evaluation matrices, detailed design |
| `04_Deliverables/` | Course submission files (.docx) |

## Conventions

- File names: `YYYY-MM-DD_Description.md` for dated records. Milestone files are named `Milestone_N[_Author].md`.
- Meeting notes follow `02_Meetings/MTG-Template.md`.
- Documents with revision history keep a `Revision History` table at the bottom.
- Terminology: PhysioMerge (PM), Danny Green (legacy software the project replaces), CCA, FMD, B-mode, CSA, longitudinal/transverse views.
- Markdown files in `00_Admin/Stakeholder_Milestones/Markdown_Files/` are converted to PDFs by a GitHub Action (`.github/workflows/generate-pdf.yml`). Don't edit anything in `PDF_Outputs/` by hand. The README folder table is also auto-updated (`scripts/update_readme.py`), so leave the `FOLDER_TABLE_START/END` markers intact.
- Mermaid diagrams are used in planning docs. Keep them valid.

## Working rules

- Don't run builds, scripts or any execution commands (user global rule). Edit text only.
- Per-person milestone files (e.g. `Milestone_1_Kyle.md`) hold one team member's assigned sections. Only write the sections the user names.
- Keep prose plain and concise. Prefer short sections and bullets over narrative. Minimal is fine where information is limited.
- Don't commit unless asked.
