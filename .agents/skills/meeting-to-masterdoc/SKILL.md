---
name: meeting-to-masterdoc
description: Parse a meeting notes file from 02_Meetings/ and update 01_Background/Established_Information/MasterDoc.md with the facts it establishes, after confirming every change with the user. Use when the user adds or names a meeting file and asks to update the master doc from it.
---

# Meeting Notes → Master Doc

Promote established facts from one meeting notes file into the master doc. The master doc is the project's source of truth, so nothing goes in without the user confirming it first.

## Inputs

- **Meeting file:** the file the user names. If none is named, use the newest file in `02_Meetings/` (check untracked/modified files with `git status` first, then modification time). Tell the user which file you picked.
- **Master doc:** `01_Background/Established_Information/MasterDoc.md`. Read the whole thing before proposing anything.

## Step 1: Check the file itself

- Compare the date in the filename with the `**Date:**` header. If they differ, flag it and ask which is right. Don't fix it yourself.

## Step 2: Classify every note

Go through the notes line by line and sort each one:

| Category | What to do |
| --- | --- |
| New fact | Propose adding it under the master doc section it belongs to. |
| Refines or replaces an existing fact | Propose rewriting the existing text, not appending a second version. Quote what changes. |
| Contradicts the master doc | Flag it explicitly as a conflict (e.g. the doc says "process in bulk" but the notes say batch processing isn't needed). |
| Contradicts another line in the same notes | Ask which is right (e.g. "scales for Doppler and ECG" vs "ECG has no scale"). |
| Possibly misrecorded | Ask (e.g. a term that doesn't fit the surrounding context, like "hypoxia" in a CO₂ discussion). |
| Changes scope status unclearly | Ask whether an item moves between core scope and bonus/extension. Never assume a promotion. |
| Opinion or suggestion, not a decision | List it under "leaving out" and ask whether a decision was made. |
| Unclear relevance | Offer the master doc's "Additional Details (May Become Relevant)" section. |
| Action items, logistics, scheduling, sentiment | Leave out. List them so the user can override. Ongoing facts behind an action item (e.g. who now owns the PM code) can still be proposed. |

Don't add technical detail beyond what the notes say. Don't interpret vague notes into confident statements.

## Step 3: Propose and wait

Present the proposal in chat and stop. Do not edit anything yet. Format:

1. Any file-level issue from Step 1.
2. **Proposed changes**, grouped by master doc section number and name (e.g. `2.2 Input Data Specifications`). Mark rewrites and conflicts clearly.
3. **Questions**, numbered, covering every conflict, contradiction, possible misrecording and scope question.
4. The "leaving out" list.

End with: "Anything you don't comment on I'll apply as proposed."

## Step 4: Apply

After the user replies:

- Apply the approved items, the user's answers and any additions they make. Treat items they didn't comment on as approved.
- Match the master doc's style: bold-label bullets (`- **Label:** text`), short sentences, sub-bullets for detail.
- Put facts in the existing section they belong to. Details about a bonus item go as sub-bullets under that item in the extensions list, not in the core sections.
- Remove or rewrite superseded text so the doc never holds two conflicting versions of a fact.
- Create the "Additional Details (May Become Relevant)" section at the end of the doc if it's needed and doesn't exist yet.
- Don't edit the meeting notes (they're raw input). If an answer reveals an error in them, tell the user where it is so they can fix it.
- Don't commit.

## Step 5: Report

Give a short summary of what changed, by section, and list anything the user should fix elsewhere (e.g. the meeting notes).
