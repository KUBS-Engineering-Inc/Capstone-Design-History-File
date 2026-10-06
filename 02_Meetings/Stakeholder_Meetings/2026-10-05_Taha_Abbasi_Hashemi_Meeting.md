# Meeting with Taha

**Date:** 2026-10-05

---

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
