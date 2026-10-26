3. PhysioMerge integration
   - **Assignee:** Kyle
   - What functions/commands can we use? How will we use them?
   - What additional features does it enable us to add to our software?

### Milestone Deliverables

**Requirements & data**

- List requirements for test harness (All)

**GUI & PhysioMerge**

- PhysioMerge recon: data handling, available commands (Kyle, Baoze)
- Write a PhysioMerge integration spec (Kyle, Baoze)
- Brainstorm video segmentation methods (Seaya / All)
  - (im assuming we mean separating the video into visual components rather than segmenting over time)
  - static parsing of location
  - dynamically find where things are bsaed on general knowledge of location but then looking for clear bounding boxes
  - dynamically finding by using mathematical readings of the screen such as variance across a frame which should be near 0 for backgrounds and static text

---

# Test Harness Requirements

These requirements are ongoing. The data has not been explored enough to know exactly what the harness needs, so they will be refined as it is.

## Purpose

A general-purpose harness for testing the functionality of the system on any ultrasound video, regardless of the procedure being performed (baseline, FMD, hypoxia, exercise, etc.). It does not need to know which procedure a video comes from.

## Requirements

- Accept any ultrasound video the system accepts as input.
- Test the system's functionality, from measurement extraction (diameter, CSA, velocity) to calculations (e.g. volumetric blood flow) and the other processing the system performs.
- Run the same tests on any video without being tuned to a specific one.
- Compare system output against ground truth where it exists.
- Report results in a form the team can review.
- Initial verification is on the FMD video.

## To be defined

- Ground truth format
- Metrics and accuracy targets
- Full list of functions under test

---

# PhysioMerge Recon

## Data Handling

- PhysioMerge (PM) expects a CSV with metadata at the top and the biometric data below. The exact format is not yet defined.
- PM automatically cleans messy signals by deleting or filtering them.
- PM records whether data was deleted as a true/false flag in the file metadata, and keeps a log of what was deleted so it can be reviewed later and is never lost. We receive this field.

## Available Commands

The commands we can use, based on what is established:

| Capability                | Purpose for us                            |
| ------------------------- | ----------------------------------------- |
| Morphology calculations   | Per cardiac cycle, so we do not redo them |
| Measurements              | Mean, systole and diastole                |
| Data deletion / filtering | Handling messy signals                    |
| `check` command           | Error correction                          |

Command names and syntax beyond `check` are not yet known.

New commands are not expected to be needed, since PM already covers what we need. If one is needed, we contribute it directly to PM so everyone benefits.

## Additional Features Enabled

PM already provides morphology calculations per cardiac cycle, which overlaps with the morphological-data extension for Doppler waveforms. No other additional features have been identified.

## Not Yet Known

- Command names and syntax
- Exact CSV format
- How PM invokes us beyond the CLI example

---

# PhysioMerge Integration Spec

## Architecture

The current pipeline is `Video -> Danny Green -> CSV -> PM`. Our software replaces Danny Green, so PM calls us directly.

## Interaction Model

- Our software is a standalone service that PM calls (e.g. via CLI). It is not called as a package or imported by PM. That said, we may make it a callable package in the future, with CLI as fallback.
- We act as a black box: PM sends input, we return output. Nothing in the interface is specific to PM, so other systems could use us the same way.
- Our application is not concerned with where the video comes from.

## Input

- Ultrasound video, provided by the caller.

## Output

- A CSV with metadata at the top and the biometric data below, which is what PM expects.
- Exact format not yet defined.

## Division of Responsibility

- **Us:** analysis of the video.
- **PM:** calculations it already provides (morphology per cardiac cycle, mean/systole/diastole measurements), data deletion/filtering and error correction via `check`.
- The final split is decided in the integration design.

## Data Deletion and Revision

- PM cleans messy data automatically and records whether data was deleted as a true/false flag in the file metadata. We receive this field.
- PM keeps the log of what was deleted, so it is never lost. We do not log deletions ourselves.
- Manual human edits keep the original machine result alongside the revision.

## Error Handling

- Error correction on messy data is done through PM's `check` command.
- Error handling needed on our end is not yet defined.

## Extending PM

If a new command is needed, it is contributed directly to PM. This is not expected.

## Open Items

- Exact CSV format
- Command names and syntax
- Invocation details beyond CLI
- Error handling on our end
