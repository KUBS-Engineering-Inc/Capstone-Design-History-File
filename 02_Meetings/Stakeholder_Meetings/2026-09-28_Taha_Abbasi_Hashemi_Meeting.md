# Meeting with Taha

**Date:** 2026-09-28

---

## Summary

- Taha walked through the duplex screen: the B-mode image, the depth scale, the green Doppler line and box, and the bottom graph with Doppler (white) and ECG (green).
- The software must handle changing or inverted scales, depth changes mid-recording, the image going off-screen, and bad data, for both baseline and protocol scans.
- Our core outputs are velocity, diameter, time and R wave. Integrating with PM gives more metrics (e.g. pulsatility index) and automated data deletion.
- Diameter must be angle-corrected. The target is the CCA, avoiding the bifurcation.
- The system is offline and will be validated against Danny Green.
- Project management: Taha wants a milestone document by Friday, a fully detailed plan by week 10, a project lead rotating every two weeks, and weekly meetings.

## Implications

M0: Timeline & Project Planning. The technical walkthrough feeds Progress Report 1: background and motivation (Ursula) and user needs and project statement (Seaya).

## Action Items

| Person | Action Items |
| --- | --- |
| Baoze | Write the M0 milestone document covering the next 13 weeks (due 2026-10-02) |
| Kyle | Write the M0 milestone document covering the next 13 weeks (due 2026-10-02) |
| Ursula | Write the M0 milestone document covering the next 13 weeks (due 2026-10-02)<br>Progress Report 1: background and motivation |
| Seaya | Lead the M0 milestone document covering the next 13 weeks (due 2026-10-02)<br>Progress Report 1: user needs and project statement |

## Notes

**Meeting Notes:**
- 3 probe ECG with no ground is also attached
- Software like Cantacia for recording ultrasound
- Scale on the left and right sides
- We need some computer vision to identify scale from the video
- We need to modify the depth on our own when we start recording, cannot assume the depth or scale are preset. Might even be inverted where negative is on top
- Graph on the bottom has pulse up (systolic point) (big point on top of graph)
- Need to identify systole and diastole on our own, and PhysioMerge is public now and will help us do this
- We should integrate PM with our code and it will reduce our workload
- ECG we also need to identify R peaks
- Must design an envelope for the graph (the bottom one with the peaks)
- Edge detection on ultrasound image and the bottom graph itself too
- Every frame, the part that we're analyzing changes. We need to analyze looking forward in time and on the frame
- Can tell if something is an artery because if you apply pressure, it does NOT collapse. Artery is higher pressure which is why it doesn't collapse but a vein would
- Venous side of blood flow will be a bit smoother rather than sharp peaks
- Windkessel effect: large arteries absorb initial kinetic energy of heart pump. Absorb as elastic energy, and then reintroduce as kinetic energy once some blood is gone. We're looking at common carotid artery which is right out of the aortic arch
- Body takes blood from the face and shoves into the brain because the brain needs constant blood flow
- We'll see a strange blood flow pattern down at the CCA but it'll be smoother up at the brain
- Moving up, bifurcation where it splits into face and brain arteries (interior and exterior carotid artery)
- Profile pattern for right before it goes into the brain looks very similar to when it's in the brain
- We want to avoid imaging the bifurcation, we need to find some green thing on the screen and once we can see it on the screen, that shows us where we need to be doing the scan
- Our computer needs to be prepared for any depth that it receives on the video (mostly just knowing the distances, unsure yet without testing how it changes the video)
- Two arteries into brain: interior carotid artery (80% of load) and posterior cerebral artery which comes from the vertebral artery
- Need to also detect depth gradient scale on the side
- Scale has colour for blood flow itself, pulses in red as blood flows through (it shows speed and direction of blood), blue is for the vein (slower and different direction)
- Vein is giant jumble of noise for the Doppler effect for its constant blood flow
- Artery is more clear
- If both vein and artery are visible in one, Doppler isn't as clear. We need to account for all the bad cases where it doesn't make full sense. Taha said it is reasonably possible to get the information we need from bad data. We'll get 30 second segment of data that needs processing
- Tool ultimately reads the waveform and video and extracts insights so relatively agnostic of the video put in
- FMD is "flow mediated dilation"
- The green line along the image shows the direction of the Doppler. The more along the angle of the flow that line is, the clearer the image
- Biphasic model we're looking at, flips between positive and negative. Negative 120 is at the top right now but we need to account for it because any negative number could be there on the graph
- Graph on bottom: Doppler and ECG. Doppler is the white and ECG is green
- He is doing a real recording for us
- We need to account for depth changing during the recording, as well as the image going completely off
- We need to find the upper, middle, and lower envelope of the Doppler
- System will never be hooked up to the internet
- Need to do baseline and protocol scans, we don't need to know which one is which, but we need project to be valid for anything
- Protocol is when we do an intervention like an FMD (when we cut off blood flow and measure during that cut off and then on release), or stuff even like depriving them of oxygen, cycling, rowing, and other things. Again we don't have to know what is happening, but the results need to be valid for all of these
- Output of data is a lot of things we don't need at the beginning (from PhysioMerge)
- Stuff important for us to provide is velocity, diameter, time, and R wave at a baseline
- Pulsatility index is sys - dias / mean. Extract many other things but PhysioMerge will give us far more options for data to give if we integrate with it
- Deleted data is true or false. Signals are messy, and especially with studies like hypoxia, you're hyperventilating, and neck is moving during the scan. Deleting the data is used there and PhysioMerge already does automated checks for deleting data
- PhysioMerge: works with one single file, says the person that you're processing data on. All anonymized names are given. It's set up in commands and he wants us to use that system. Stuff like after you read data, you filter data (not that we're filtering but same idea)
- He wrote something that finds the minimum point in waveforms
- We can process data after and make the measurement that we like, and calculations themselves are done in the system
- When the data is being run, you can see what it's extracting. It can run in real time so is quite slow
- Arteries are all sloped, so vertical distance is wrong and we can't use that. We need to account for the angle of the artery
- Need to find the box (green thing telling you where the recording is) from the video we're provided. Then take measurements around that

**Project Management:**
- He wants to know who is doing what and milestones for us
- At the end of winter semester (week 13), we do write up. He wants plan finished by week 10. Want detailed plan of everything that is going to happen and how. All libraries used, everything planned in advance, what we're doing, how, and it will make the implementation a lot easier by having it all planned beforehand
- Every two weeks, one of us is the project lead and responsible for deliverables of that week
- Want a plan done as each week comes
- Winter semester is execution at the start and then testing and verification
- See how it integrates with other things and test as much as we can
- Danny Green software is what we're testing against
- We can do weekly meetings at this time

**Action Items:**
- By Friday, have milestone document with everything we will be doing for the next 13 weeks and basically describing how we'll achieve that fully fleshed out plan by the end
