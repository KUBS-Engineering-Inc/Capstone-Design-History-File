# Meeting with Taha

**Date:** 2026-09-17

---

- How did Danny Green's training go? needs more time on it
- The CD box at the top of Danny Green has issues and doesn't show something accurates
- Probably needs more questions
- Dr. Baara is most experiences person on our ultrasound
- Talking about things we could use the ultrasound other than just the lab
- Asked Dr. Baara if we're talking to the other labs about the ultrasound usage
- We take camtasia videos, but the terason supports videos of itself
- Why don't we just use that. It supports dichom videos
- Medical images (e.g. MRIs), has embedded values of history all tied to the image. It has metadata. Very useful for medical imaging. Nice thing about is there are a lot of toolboxes that can be used to analyze Dichom files. Matlab, R. Raw data on terasim will be saved as the metadata. We normally use camtasia (the screen recording software). We can set up a patient file (TTSA_001). Saves it as a series of B-mode images. You can export it as a sinoloop (chinese loop?). Dichom viewer can see everything frame by frame afterwards. You do image analysis on the raw data that way.
- image j
- some built in image analysis toolboxes that are built into python for dichom
- Homework: looking at ultrasound dichom image analysis toolboxes in python. This has been done for decades. Better than using image capture like this. The raw data is the video itself rather than the actual video. How is this different than the video?
- there are tools out there that we can use that will be betteer than what we're using
- The angling of the vessel and diameter.

- kyle presents
- what milestone 2 is. getting area diameter and the angle. throwaway tests. 

- we get the current max envelope
- we want the average envelope is what we would multiple by the area to get flow
- the outer envelope is the gate over only the middle of the vessel
- true flow is actually the average of all the velocities times the area to get us flow
- The max envelope is fine. What we do right now since it's difficult to get the average. We assume that the peak is twice as high at the middle. We assume a perfect parabolic shape in vessels, so we take the peak and then divide it by two. multiple by area and then get the flow.
- Other ways where when you collect the full spectrum through the labchart file, you can just average the data over time. if theres a way to capture all the velocities. Average across all the spectra would give us closer to mean velocity.
- parabolic assumption breaks down when you have bifurcations and changes where you're looking
- volumetric is over time. you have diameter over time and spectral velocity. You would time align match them and multiple them by mean velocity. Mean over one time scale. a spatial mean
- are you taking diameter over three minutes and then velocity over three minutes and then average and multiply, but this is not as good since we have the specific thing
- find the middle or average across

- We're assuming equal worth for every single velocity. Does the brightness of the pixel tell us anything. The spectral intensity matters more in a mean calculations. Think about how we translate from the full spectrum into a representative velocity.
- There are some ultrasound resources that Baara will send so we understand the ultrasound foundations
- look at the brightness and have it intensity-weighted
- are you comfortable diving into literature to know how it's been done? yes we are

- Something to think about is the resolution. Because we're looking at resolution, do we know how much resolution we've lost moving over to the camtasia video recording. How do we change back into the real values. What would the raw data look like and what have we lost. We ideally take diachom and compare it with the mp4 in same session.
- good to know what is the resolution of the images we're looking at.
- this is awesome, and there are no other questions. Taha is very passionate about the phys-engineering interface
- having fun in how we're navigating the problem. align yourself also so that we're not recreating something that's already been done.

straight forward questions
- range on the depth of the ultrasound? wants to say 12 cm but the ultrasound got given away to a differnet lab. terascon usmart 3300 with the linear probe
- 3 cm and 4 cm we looked at. Does this increase linearly?
- updates on getting access to the physiomerge code? taha sending that email now
- for decreasing the cursor gates, how small can you make that cursor? never has tried it before. very small. 

currently we're unable to publish anything that we have done
- we'll be put onto his study. and then because we're on the ethics, and then we can publish. We will be able to use the data from other people. Data diversity up, and there are undergrad conferences that we can present at
