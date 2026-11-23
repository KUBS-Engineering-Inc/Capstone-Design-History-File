---
name: meeting-to-masterdoc
description: Parse a meeting notes file from 02_Meetings/, update 01_Background/Established_Information/MasterDoc.md with the facts it establishes, and add a Summary, Implications and Action Items section to the meeting file, after confirming every change with the user. Use when the user adds or names a meeting file and asks to update the master doc from it or clean it up.
---

# Meeting Notes → Master Doc

Promote established facts from one meeting notes file into the master doc, and add a summary, milestone implications and action items to the meeting file. The master doc is the project's source of truth, so nothing goes in without the user confirming it first.

## Inputs

- **Meeting file:** the file the user names. If none is named, use the newest file in `02_Meetings/` (check untracked/modified files with `git status` first, then modification time). Tell the user which file you picked.
- **Master doc:** `01_Background/Established_Information/MasterDoc.md`. Read the whole thing before proposing anything.
- **Milestone timeline:** the "Stakeholder Milestones" and "Course Deadlines" tables in `00_Admin/Stakeholder_Milestones/Markdown_Files/Milestone_0.md`.
- **Target milestone:** see Step 1.

Any meeting file works, including old ones. All milestone logic uses the meeting's date, not today's date.

## Step 1: Check the file and find the target milestone

- Compare the date in the filename with the `**Date:**` header. If they differ, flag it and ask which is right. Don't fix it yourself.
- Using the Stakeholder Milestones table, work out two milestones relative to the meeting date:
  - **Just finished:** the most recent milestone whose end date is on or before the meeting date and no more than 7 days before it. There may be none.
  - **Target ("next") milestone:** the milestone after the just-finished one. If none just finished, the milestone in progress on the meeting date.
- Stakeholder meetings usually happen just after a milestone is due, to update the stakeholder on it. So the just-finished milestone gives context for what was discussed, and the target milestone is what Implications and Action Items are about.
- If there's no milestone after the just-finished one, or the meeting date falls outside every range, say so and ask which milestone to target. Don't guess.
- Read the target milestone's section under "Milestone Planning" in `Milestone_0.md` (deliverables, assignees, due date), and do the same for the just-finished one if there is one.
- Read the milestone files in `00_Admin/Stakeholder_Milestones/Markdown_Files/` for both: `Milestone_N.md` and any per-person `Milestone_N_<Author>.md`. Skip `*_Archive.md`. If a milestone has no file yet, use its `Milestone_0.md` planning section alone and say so.
- Note any course deadline from the Course Deadlines table that falls within the target milestone or shortly after the meeting.

## Step 2: Classify every note

Go through the notes line by line and sort each one:

| Category | What to do |
| --- | --- |
| New fact | Propose adding it under the master doc section it belongs to. |
| Refines or replaces an existing fact | Propose rewriting the existing text, not appending a second version. Quote what changes. |
| Contradicts the master doc | Flag it explicitly as a conflict (e.g. the doc says "process in bulk" but the notes say batch processing isn't needed). |
| Older than the master doc content it touches | When processing an old meeting, a master doc fact may come from a later meeting. Check `git log` on the master doc and the dates of other meeting files. If the master doc is likely newer, don't propose reverting it; list the note as superseded and ask only if unsure. |
| Contradicts another line in the same notes | Ask which is right (e.g. "scales for Doppler and ECG" vs "ECG has no scale"). |
| Possibly misrecorded | Ask (e.g. a term that doesn't fit the surrounding context, like "hypoxia" in a CO₂ discussion). |
| Changes scope status unclearly | Ask whether an item moves between core scope and bonus/extension. Never assume a promotion. |
| Opinion or suggestion, not a decision | List it under "leaving out" and ask whether a decision was made. |
| Unclear relevance | Offer the master doc's "Additional Details (May Become Relevant)" section. |
| Action items, homework, follow-ups | Keep out of the master doc. Use them for the Action Items table (Step 3). Ongoing facts behind an action item (e.g. who now owns the PM code) can still be proposed for the master doc. |
| Logistics, scheduling, sentiment | Leave out of the master doc. List them so the user can override. They can still inform the Summary. |

Don't add technical detail beyond what the notes say. Don't interpret vague notes into confident statements.

## Step 3: Draft the meeting file sections

Draft three sections for the meeting file. They are drafts until Step 5.

### Summary

- Key takeaways from the meeting: decisions, new information, feedback.
- Bullets, one line each. Only what the notes say.

### Implications

- What from this meeting matters for the target milestone, judged against the master doc, the milestone planning section and the milestone file(s).
- Examples: a note that changes or confirms a milestone deliverable, affects a design decision the milestone is finalizing, contradicts something already written in the milestone file, or touches an upcoming course deadline.
- Name the milestone (e.g. "M4: Final Implementation Plan") at the start.
- Write a short paragraph if there are one or two points. Use bullets for three or more.
- If nothing is relevant to the target milestone, say so in one sentence.

### Action Items

- Table with one row per team member, always in this order: Baoze, Kyle, Ursula, Seaya. All of a person's items go in their single cell, separated by `<br>`.

  ```markdown
  | Person | Action Items |
  | --- | --- |
  | Baoze | Item one<br>Item two |
  | Kyle | Item one |
  | Ursula | Item one |
  | Seaya | Item one |
  ```

- Notes rarely make owners or tasks clear. The default item for each person is "Work on M<N>: <milestone name>" for the target milestone.
- Don't invent tasks or assign owners yourself. Draft only what the notes state outright, and turn everything else into questions (Step 4).
- Ask about anything discussed that could lead to work, e.g. homework the stakeholder set, follow-ups someone offered, open questions the team has to answer, or milestone deliverables the meeting touched. For each, ask whether it's an action and who owns it. Also ask about each person's assigned deliverables for the target milestone.
- If the file already has an Action Items section (e.g. from the template), keep its existing items and merge into the new table.

## Step 4: Propose and wait

Present the proposal in chat and stop. Do not edit anything yet. Format:

1. Any file-level issue from Step 1.
2. **Milestone check (flag clearly, first thing after file issues):** the just-finished milestone (or "none") and the target milestone, with their date ranges and the file(s) you read, e.g. "Meeting 2026-11-23: M3 ended 2026-11-20 (just finished), so targeting M4 (2026-11-21 to 2026-12-04). Correct me if the schedule has shifted."
3. **Proposed master doc changes**, grouped by master doc section number and name (e.g. `2.2 Input Data Specifications`). Mark rewrites and conflicts clearly.
4. **Draft meeting sections:** the Summary, Implications and Action Items table as they would be written.
5. **Questions**, numbered, covering every conflict, contradiction, possible misrecording and scope question, then the action item questions.
6. The "leaving out" list (master doc only).

End with: "Anything you don't comment on I'll apply as proposed. Action items you don't answer stay as the milestone default."

## Step 5: Apply

After the user replies:

### Master doc

- Apply the approved items, the user's answers and any additions they make. Treat items they didn't comment on as approved.
- Match the master doc's style: bold-label bullets (`- **Label:** text`), short sentences, sub-bullets for detail.
- Put facts in the existing section they belong to. Details about a bonus item go as sub-bullets under that item in the extensions list, not in the core sections.
- Remove or rewrite superseded text so the doc never holds two conflicting versions of a fact.
- Create the "Additional Details (May Become Relevant)" section at the end of the doc if it's needed and doesn't exist yet.

### Meeting file

- Rewrite the Action Items table from the user's answers. Make each item a concrete task. Keep the default milestone item for anyone who got no specific items.
- Revise the Summary and Implications if the user's answers change them.
- Insert the sections directly below the header block (title, date and the `---` after it), above the raw notes, in this order: `## Summary`, `## Implications`, `## Action Items`. Add a `## Notes` heading above the raw notes if they have no heading.
- If any of these sections already exist (the skill was run on this file before, or the template was used), update them in place rather than adding duplicates.
- Don't change the raw notes or any appendix. If an answer reveals an error in the notes, tell the user where it is so they can fix it.

Don't commit.

## Step 6: Report

Give a short summary of what changed in the master doc (by section) and in the meeting file, and list anything the user should fix elsewhere (e.g. errors in the raw notes, or a milestone file that conflicts with what was established).
