---
name: update-folder-guide
description: Update the "What's in Each Folder" section of the root README.md so it matches the folders and key files actually in the repo, after confirming the changes with the user. Use when folders are added, renamed, moved or removed, or when the user asks to refresh the folder guide.
---

# Update "What's in Each Folder"

Keep the hand-written `## What's in Each Folder` section of `README.md` in sync with the repo. The GitHub Action (`scripts/update_readme.py`) only regenerates the top-level table between `<!-- FOLDER_TABLE_START -->` and `<!-- FOLDER_TABLE_END -->`; this section goes one level deeper and has to be kept up to date by hand.

## Rules

- Only edit the `## What's in Each Folder` section, plus one row in the README's `Revision History` table. Never touch the text between the `FOLDER_TABLE` markers or the `FOLDER_TABLE` markers themselves.
- Describe only what is in the repo. Don't invent folder purposes; if a folder's purpose isn't clear from its name and contents, ask the user.
- Don't run scripts or builds. Reading the repo with `git` and file tools is fine.
- Don't commit.

## Step 1: Read the current state

1. Read `README.md` and find the `## What's in Each Folder` section. If it doesn't exist, it goes right after `<!-- FOLDER_TABLE_END -->`.
2. List what's committed: `git ls-files`. Note the folders two levels deep (e.g. `03_Design/02_Design_Decisions/`) and any notable single files at the first level (e.g. `00_Admin/ToolsInstallationGuide.md`, `02_Meetings/MTG-Template.md`).
3. Check `git status --short` for untracked or new folders. They aren't in the repo yet; list them separately and ask whether to include them.
4. Ignore `.git/`, `.gitkeep` files, and anything the README's folder-table script ignores.

## Step 2: Compare

Sort every difference between the section and the repo:

| Difference | What to do |
| --- | --- |
| Folder in the repo but not in the section | Propose a bullet for it. Base the description on its file names and, if needed, a quick read of one or two files. |
| Folder in the section but no longer in the repo | Propose removing it. Check first whether it was renamed or moved (a similar folder elsewhere); if so, propose updating the bullet instead. |
| Description no longer matches the contents | Propose a rewrite and quote the old text. |
| Untracked folder (from `git status`) | Ask whether to include it. |
| Purpose unclear | Ask the user. |

## Step 3: Propose and wait

Show the proposed changes in chat and stop. Don't edit yet. List additions, removals and rewrites, then any questions, and end with: "Anything you don't comment on I'll apply as proposed."

## Step 4: Apply

- Keep the existing style: one top-level bullet per root folder in repo order, `- **\`folder/\`**: short description.`, with sub-bullets for its sub-folders and key files (`` `Sub_Folder/`: description``).
- Keep descriptions to one short line. Mention files only when a reader needs to know about them (templates, the master doc, auto-generated folders that shouldn't be edited by hand).
- Add a row to the README's `Revision History` table: today's date, the next minor version, and "Updated folder contents section".
- Don't change other sections of the README. If something else looks out of date (e.g. links to folders that don't exist), tell the user instead.

## Step 5: Report

Summarize what was added, removed and rewritten, and list anything outside this section the user should look at.
