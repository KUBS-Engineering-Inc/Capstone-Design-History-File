# Milestone 1: Component Prototyping & Design Outputs

**Created:** 2026-11-21

# Desired Error States

These are states that we do not have recorded and must procure in order to fully test the error handling of our system.

- mouse resting over important items
  - scale lines (bmode and spectral)
  - scale numbers (bmode and spectral)
  - middle of vessel
  - vessel wall
  - z line
  - doppler waveform
  - ecg
- vessel nonexistent (e.g., offscreen)
- vessel blurry
- multiple vessels visible (multiple of this, various levels of focus and where they appear on screen)
- unclear spectra (e.g., out of focus and super large peaks)
- change of depth (so we can see how the scale changes as well as how the image changes)
- change of scale in doppler waveform
- z-marker in a weird place (far away from where we're measuring)
- insonnation angle not very parallel to wall
- structures that look similar (e.g., jugular, thyroid)

# Already existing error or abnormal states

- patient laughing
- patient coughing
- thin vessels (Ursula's image from her arm which has smaller veins than neck)
- ecg absent
- colour on vessel for doppler

# Transition States

These states signify any transition of a view from view A to view B.

- bmode only to bmode + spectral
- bmode only to M mode
- bmode + spectral to bmode only
- M mode to bmode only
- bmode + spectral to M mode
- M mode to bmode + spectral

Within these states, we must assume that it is also possible that potential error states can occur. For example, switching modes at the same time that the scale switches.
At least one error state should be recorded in conjunction with at least half of the transition states outlined above.
