# Melvin Feedback

Graded meeting with software TA

**Date:** 2026-11-26

---

# Agenda

- Say hello
- Give an update on the data we collected
  - Dichom didn't work
  - Doppler waveform reconstructed successfully
  - New UI flow
- Data acquisition update: Kyle figured out error and transition states, all of which we recorded to ensure we can test every edge case. Shoutout See-ya for recording the timestamps at which every error/transition occurred.
- We're now researchers at Mac, not yet inventors. Can get more data from there, but none technically needed at this point.
- Discuss how we have modules for the test cases and a semi-unified framework for running them all
- POC Demo
  - what they want us to talk about in terms of next steps - full layout or general ideas?
  - is feasibility of throwaway tests good enough for feasibility and risk analysis part of rubric
    - spencer and other instructor would be in charge of this, in his opinion, it's better to have a bunch of tests that verify that our application/entire system will behave properly in ways that we describe one-by-one
    - "based on these metrics and these tests, we are confident our app will work".
    - better to have small wireframe for ui
  - how put together do they want things in the demo to be? (code-wise)

---

# Notes

- asked about stuff like where we're deploying, we said just a local python app, dearpygui is our top choice for the gui
- 4 main focuses this term
  - solidifying error states and transitions
  - solidifying ui states
  - correcting how we measure doppler
  - creating testing harness
- next steps
  - annotating data, getting danny green comparisons
  - getting mockups on ui
  - comparing max and mean methods for doppler waveform
  - defining how test cases will work and we'll define thresholds
- our progress is satisfying
- need to be careful about data annotation, it can be done incorrectly quite easily
- may not need a fancy ui for them, so we still need to put some effort and it's good to include but up to us
-
