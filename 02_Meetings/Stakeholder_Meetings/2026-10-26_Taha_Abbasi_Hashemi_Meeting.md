# Meeting with Taha

**Date:** 2026-10-26

---

## Summary

- The team presented M1, and Taha was very positive.
- FMD and CBF are use cases of the core measurements. FMD needs diameter, velocity and flow.
- CSA detection works the same for arteries and veins, but the test harness should test both.
- When both an artery and a vein are visible, that's noisy data: the software estimates the target and the operator can switch.
- OpenCV is the research standard; we're going with that.
- Screen layout:
  - Scales are always in the same place, and ECG has no scale.
  - The sidebar shows BPM when ECG is on.
  - Taha explained the Z marker's parts. The marker isn't always present.
  - B-mode, M-mode and pulse wave are separate modes.
- The insonnation angle should be calculated relative to the vessel walls.
- PM is now owned by the university. Code access goes through Milo, and Taha will email him and cc us. Batch processing isn't needed.

## Implications

M2: Research & Design Planning.

- **OCR throwaway tests (Kyle):** search fixed regions of interest for the scales. The sidebar text can be read with OCR. ECG has no scale.
- **Wall detection and angle-corrected diameter (Seaya):** use the Z marker's geometry and compute the insonnation angle relative to the vessel wall. Handle the case where the marker is missing.
- **Segmentation comparison (Seaya):** OpenCV vs PyAV.
- **Test harness design (Ursula, Seaya):** test CSA on arteries and veins separately.
- **UI states (Baoze):** the operator needs to be able to switch the target vessel.
- **Graded advisor meeting:** 10-29, three days after this meeting.

## Action Items

| Person | Action Items                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Baoze  | Doppler: track the timeline from timestamps<br>Transverse: detect circular vessels<br>Define UI states (process, edit, pause, cancel, undo), including switching the target vessel<br>Wireframe the UI and start the Figma overlay, with Seaya                                                                                                                                                                                                                             |
| Kyle   | Doppler: OCR the scale, searching fixed regions of interest (ECG has no scale)<br>B-mode: OCR the depth scale                                                                                                                                                                                                                                                                                                                                                              |
| Ursula | Doppler: extract the waveform and its envelope<br>Doppler: separate the ECG and detect R-peaks<br>Design the test harness, with Seaya, testing CSA on arteries and veins separately                                                                                                                                                                                                                                                                                        |
| Seaya  | Compare segmentation methods, including OpenCV vs PyAV<br>Throwaway test: segment fixed regions on the test dataset<br>Design the test harness, with Ursula<br>Longitudinal: detect artery walls<br>Longitudinal: calculate angle-corrected diameter, with the insonnation angle relative to the vessel wall and handling a missing Z marker<br>Wireframe the UI and start the Figma overlay, with Baoze<br>Team contact with Taha for PM code access (Taha contacts Milo) |

# Raw Meeting Notes

- finished milestone 1, telling taha about it
- don’t worry about fmd, it’s just a type of scan like CBF. its a use case
- for fmd, we need diameter, velocity, and flow
- csa should be fundamentally identical for artery vs vein in terms of computational edge detection, but we should still test both in our test harness
- for a vein and artery visible, that’s considered noisy data. We have the target vessel in the video data itself so we’d just make sure that we detect the right one (maybe if both are visible, estimate which is the right one but the operator can choose the other one if needed)
- co2 levels change ultrasound because it’s a prominent dilators for blood vessels so that’s what co2 tests are, with hypoxia, blood vessels get bigger over time
- we’d do hypercapnia and hypocapnea for increased and decreased co2
- HE SAID “THIS IS SO GOOD I LIKE THIS SO MUCH” 🥹🥹🤩🤩🤩
- opencv is research standard in his experience, but he’s interested in the fact that pyav has more control over ffmpeg commands and libraries unavailable in opencv
- scales for Doppler and ecg always appear in same location, so we’re thinking of just searching the given area for the scale where we know it would appear (searching regions of interest)
- can ocr text one side since it’ll say different things
- another mode shows the bottom graph where there’s a line on the ultrasound and the bottom graph shows a snapshot along the line at a given depth over time.
- regular M mode has no marker
- marker always appears when there’s velocity of something
- long line is vertical, two parallel lines is the region of interest, and the diagonal line going through them to make a z (the smaller dotted one) is insonnation angle of the angle the Doppler is going at. So Doppler effect at certain depth is reading between the two lines inside that region. So insonnation angle should be parallel to vessel wall
- he wants us to calculate angle of it relative to vessel walls
- right side has info about probe, like depth, current angle of insonnation (not relative to vessel wall but the actual machine inside the operator thingy that is sending the waves)
- M mode is available transverse and longitudinal
- M mode and B mode are different and their functionalities are diff. So M should be able to do what M needs to do and B too.
- pink marker on right side of ultrasound video is the “focus”, so it shows where along the graph has the most focus (unsure if relevant to us)
- B mode is always there. Always on. It’s the video that we see. M mode is the view of the line over time where the line shows on the B mode video. Doppler mode is called pulse wave which shows up on the bottom graph, same as the M mode graph.
- so full screen is just B mode, and scale is just on the right side of it. If there’s a graph in the bottom left, we can detect that and it means pulse wave or M mode is active. The text on the graph is what tells us which mode is active. There might also be a text indicator in the bottom part of the screen that says which mode is active.
- ecg has no scale
- right side of screen with the general data also shows bpm when ecg is active
- the z thingy won’t always be there so we will have to find the region of interest if it doesn’t exist
- side bar is always there
- we need to talk to Milo, Taha is no longer code owner. The university now owns physiomerge so we need to talk to this guy to get the code. Taha will send an email and cc us
- Taha is getting a learning session Thursday on how to use Danny green.
- he doesn’t need batch processing but we can try it at some point
- we’re recording diameter, cross sectional area, Doppler, ecg, and feed all that data to PM. stuff like error checking is already done by PM.
