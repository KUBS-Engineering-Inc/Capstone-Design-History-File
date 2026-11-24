# Meeting with Taha

**Date:** 2026-10-05

---

## Summary

- The team presented the M0 plan, and Taha liked it.
- PM integration:
  - We use PM v2, but its documentation is for v1.
  - We integrate through PM's commands; we shouldn't need new ones.
  - Taha prefers PM to call our software, e.g. through a CLI.
  - PM's input is a CSV with metadata on top.
  - Commands of interest: `morphology`, `measurement`, `check`.
- Manual edits need a revision history that keeps the original machine result.
- Some users want a GUI, but a CLI is welcome too.
- Hardware: RTX A5000 GPU, Xeon W-2245 CPU, 32 GB RAM. We should have a fallback.
- Recordings have a constant frame rate. File sizes are about 6 GB per 30 minutes and 12 GB per person.
- The software must handle the transverse view without Doppler, a changing time scale, flicker, and patient coughing, laughing or hyperventilating.
- Liz knows the Danny Green software.

## Implications

M1: Preliminary Research & Design Inputs.

- **PM recon and integration spec (Kyle, Baoze):** focus on `morphology`, `measurement` and `check`. Remember the docs are for v1 while the code is v2. PM calls us (CLI), not the other way round.
- **Hardware constraints (Baoze):** confirmed here; already recorded as C.ENV-1 to C.ENV-4.
- **UI and output requirements:** revision history (F.OUT-11) and CLI access (F.OUT-9) come from this meeting.
- **Robustness cases (Seaya):** no Doppler, flicker, patient movement, and a changing time scale.
- **Danny Green research (Ursula):** Liz is a possible contact.

## Action Items

| Person | Action Items |
| --- | --- |
| Baoze | Research Doppler ultrasound (B-mode, Doppler, FMD)<br>Determine hardware constraints (GPU/CPU, real-time)<br>PM recon and integration spec, with Kyle<br>Design the test dataset with ground truth, with Ursula and Kyle<br>List UI, output and test harness requirements (all) |
| Kyle | Research PM integration: `morphology`, `measurement` and `check` (docs are v1, code is v2)<br>PM recon and integration spec, with Baoze<br>Design the test dataset with ground truth, with Baoze and Ursula<br>List UI, output and test harness requirements (all) |
| Ursula | Research Danny Green's software<br>Write the validation test plan against Danny Green<br>Design the test dataset with ground truth, with Baoze and Kyle<br>List UI, output and test harness requirements (all) |
| Seaya | Research image processing tools<br>List image processing requirements and robustness cases (no Doppler, flicker, patient movement, changing time scale)<br>Brainstorm video segmentation methods<br>List UI, output and test harness requirements (all) |

# Raw Meeting Notes

- Seaya flounders for her outlet
- Seaya killing it with the milestone description
- Taha said “that’s really good”
- physiomergr builds csv file in real time
- we’re using version 2 with similar commands to v1 but documentation is all v1
- morphology features Python file basically just uses other features and files to run
- he uses class models
- to integrate with physiomerge, all we need to do is create new command that goes in commands file
- build command based on parameters (we shouldn’t need new commands)
- wants us to build something that integrates with physiomerge, probably pass in file through cmd argument to use it (so CLI access for PM)
- revision history is a good idea for any manual human edits, keep original machine result
- input into physiomerge is a csv, has some metadata up top and then has the actual biometric data lower down
- current setup is video -> Danny software -> csv -> physiomerge
- he likes us passing in memory to physiomerge if possible, it also allows for metadata to be kept separate
- we can call physiomerge as a package
- he prefers physiomerge being the one to call us, so we may just produce a file output that physiomerge reads to directly replace Danny green, or we find another way for physiomerge to call us that doesn’t produce the intermediate file and also lets us know which physiomerge commands to use for data extraction (since he said they have a bunch of built in commands to get information that we’ll need in our software)
- people like Michelle will still enjoy a gui, but we can support cli if it works anywhere
- bounding green Z box in video tells us where to start looking but then we bfs to find the vessel walls around it somewhere
- command documentation is the same from v1 now in v2. Of interest: morphology (calculates all morphology in one cardiac cycle) and measurement (calculates mean and systole and diastole and stuff)
- device has nvidia rtxA5000 and xeon w-2245 CPU. probably should have a fallback
- error correction or checking should be done through physiomerge’s check command
- recordings are constant frame rate
- Has met Danny Green
- ECG
- New view
- No Doppler in this view
- Test for pregnancies
- Look for lub dub
- Flicker yes
- You want it the size of the artéy, Doppler should be parallel as much as you can
- Yes to be able to handle no Doppler
- Colour with pulse wave less priority
- Time scale can also change
- Stuff that happens during ultrasound, cough, hyperventilate, laugh
- Liz knows Danny Green software
- 32 gbs
- 12 per person for hours
- 6 gigs for 30 mins
