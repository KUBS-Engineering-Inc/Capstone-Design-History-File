# Meeting with Taha

**Date:** 2026-11-23

---

## Summary

- Taha likes the UI overall.
- The team told Taha that some deliverables were changed because they made less sense than planned.
- IP: McMaster University will officially consider the team "Inventors" of our software, which is separate from PM. PM-related work is done under Taha's supervision, and the team signs a form stating it didn't invent PM.
- A proposal to add the team to the study has been submitted to HiREB. The team should be on the study by 11-30.
- The team can join data collection as subjects or as experimenters (tilt table, charting software), booked 6am to noon.
- Danny Green problems: vessel bounds are adjusted while the video keeps playing, playback speed depends on the CPU, and there's no pause. Our software needs full playback controls.
- In Danny Green, manual adjustment applies to the ROI, not the vessel wall. Wall detection is fully automatic.
- Automated vessel detection is the preferred route. Tolerance ideas (not decided):
  - Seaya: show a grid of how various tolerances change the edge detection; the user selects the one that looks best, and it propagates.
  - Kyle: likes the grid, but the user should also be able to fine-tune it further (e.g. slider or text input).
- Bad data: process it as if it's good and don't flag it. PM decides what to do with it.
- PM reads each system's output through a Python reader file. Danny Green's output is a CSV with metadata, a header row, then the data. We'd add a reader file for our output CSV; this is separate from how PM calls us.
- DICOM records only the last 10 s, so stick with MP4 (Camtasia). DICOM is a far-future extension.

## Implications

M4: Final Implementation Plan.

- **PM integration design (All):** our output CSV can follow Danny Green's structure (metadata, header row, data), with a new PM reader file configured for it. Bad data isn't flagged on our side. PM-facing work is done under Taha.
- **UI (Baoze):** full playback controls (pause, fast forward, speed independent of CPU) are now a requirement. How manual adjustments work is still undecided.
- **B-mode design (Seaya, Kyle, Baoze):** automated wall detection is the preferred route; the tolerance grid is an open idea.
- **Extensions feasibility (All):** DICOM moves to far-future.
- **M3 error-state list:** the "dicom video" item in `Milestone_3.md` is now low priority.
- **Course deadlines:** Advisor Meeting 2 is on 11-26 and the POC demo is on 12-03.

## Action Items

| Person | Action Items |
| --- | --- |
| Baoze | Finalize the UI, including full playback controls<br>Finalize B-mode design, with Seaya and Kyle<br>PM integration design, final design document, demo and extensions feasibility (all) |
| Kyle | Get a sample Danny Green output CSV to model our output on<br>Discuss the tolerance-selection grid further, with Seaya<br>Finalize Doppler design, with Ursula<br>Finalize B-mode design, with Seaya and Baoze<br>PM integration design, final design document, demo and extensions feasibility (all) |
| Ursula | Follow up with Taha on whether Dr. Baraa can save full DICOM videos<br>Finalize Doppler design, with Kyle<br>PM integration design, final design document, demo and extensions feasibility (all) |
| Seaya | Discuss the tolerance-selection grid further, with Kyle<br>Finalize B-mode design, with Kyle and Baoze<br>PM integration design, final design document, demo and extensions feasibility (all) |

## Notes

- told him that some deliverables didn’t make as much sense so we modified what we were doing
- he likes the ui overall
- asks what we’re demonstrating. We explain POC demo for class
- asks where we are for the POC demo. We explain its just a POC, not rigid presentation structure
- they had a big meeting with MILO, told them what our group is doing here. Likely we will have our group be our own inventors of this new software, “unrelated” to physiomerge. Anything done applying to PM is done with Taha and we sign a form saying that we didn’t invent PM. so by the end of the year, we’ll be considered “inventors” which McMaster university. So we can still do work that integrates with PM but it’s all officially done with taha’s supervision
- with Hirep, they submitted a proposal for us to be on the ethics team, currently waiting on that. By Monday we should officially be on their research study.
- we can be part of data collection both as subjects and experimenters. Taha would run the experiment and if we’re helping out, we would be in charge of the tilt table or charting software. They have a calendar to book in, anytime from 6am-noon
- with Danny green, you move the vessel bound in real time WHICH SUCKS. you’d move it, frames would continue. If your cpu is slow/fast, it would go at that speed, so you couldn’t control the speed at which it goes. No pausing or anything. They need all that improved.
- people like the manual adjustment of blood vessel selection but automated is the best route. Seaya wants to show a grid of tolerances where they choose the best one that looks like it finds the vessel walls. Then that tolerance propagates (I say we let the tolerances adjust over time though)
- Taha clarified that manual adjustment is of the ROI and not vessel wall itself. Danny green lets them choose the ROI that is analyzed but the users get no control over vessel wall detection
- if there’s bad data, “do what you can”, treat it as if it’s good, and PM chooses what to do with the data. So don’t bother flagging the data or anything, just process it the best that we can.
- first version of PM Taha wrote himself. Second one was fully vibe coded. He was curious if he could redo everything that he’s done. It’s too big of a program to really vibe code so you do stage by stage
- how PM works: different read parts functions that define how to integrate with various systems and read their data. We’d just make a new Python file to define them reading from our source. Output from Danny green is a csv with some top level metadata and the actual data x rows down with a header and then the data itself. The Python file to read from it just defines how to read that data, so we’d do something similar with ours.
- for the time being, dicom won’t work because it only records last 10 seconds, so Taha will ask Baraa if we can save the full video. So stick to mp4 camtasia. Consider dicom and using any metadata an extension we think about way in the future

# Appendix - Error State Video Timestamps

Recordings were taken of Baoze over all the identified error states in milestone 3. The following is a comprehensive list of the states we identified and the timestamps around which they occurred.

```
0016 - covering up text and scale lines
0050 - covering spectral scale lines
0115 - cover doppler itself
0135 - cover doppler cursor and wal
0150 - vessel blurry
0200 - vessel gone
0120 - 2 vessels
0330 - inverting doppler
0350 - doppler showing 2 vessel forms
0430 - doppler out of focus
0437 - doppler with large peaks
0450 - blurry doppler
0515 - min b mode 2 cm
0540 - waveform at bottom (opposite of x axis)
0630 - zooming out for depth to max of 12 cm
0720 - changing velocity scale of doppler
0810 - velocity scale max
0840 - changing frequency of the doppler pulses (what does that do tho)
0905 - cursor is off image
0920 - image is also not good
0940 - spectral different colour
1000 - b mode different colours
1020 - cursor not green
1045 - cursor off - spectral auto disappears
1130 - bad insinuation angle
1150 - m mode
1215 - changing sweep speed for m mode
1250 - changing sweep speed for doppler
1330  - laughing
1340 - coughing
1350 - rrrrrr
1400 - transverse
1436 - ballooning of the vein close
1445 - more ballooning
1500 - vein reacting to pressure increase and decrease
1520 - multiple rois
1550 - removed probe
1615 - returned probe
1640 - vertebrae
1720 - vessel enlargening as we approach aorta
1745 - many vessels
1750 - transverse view (2d in footer)
1820- multiple in transverse geow
1825 - coughing
1840 - mouse cursor on screen
1900 - m mode systole slow transverse
2000 - darkening/lightening ultrasound window
2020 - dynamic range of ultrasound window
2110 - adjust persistence
2130 - trapezoidal view
2140 - doppler trapezoidal
2240 - editing with omnibeam
2300 - editing with tb level
2310 - editing mapping
2320 - flipping
2340 - inserting needle
2410 - rulers (center mark blue line)
2420 - horizontal ruler
2455 - dicomming
```
