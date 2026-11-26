# UI Flow Diagram Iteration 1 - Notes
## Stakeholder Notes
- Approves of the general flow
- Makes note that a cmd line operation works, but current users of Danny Green's software would prefer a GUI and similar functionality
- On manual editing:
  - We previously understood manual editing to mean something along the lines of dragging the lines defining the vessel walls up/down for more accurate capture of vessel based on user knowledge
  - HOWEVER: actual functionality is constrained to only changing the edges of the "bounding box" which defines the search area
- CSV best output option - can consider other direct links with PhysioMerge in future

## Application
- Bounding box editing:
  - Not directly compatible with our lumen-based search technique
  - However we can highlight / identify a center point of our vessel ROI that user's can change
    - With doppler cursor defined ROI -> highlight intersection point of insonation line & doppler beam line
    - Without doppler cursor -> calculate center point of ROI(s) and highlight those
    - With dopple cursor + secondary ROIs -> highlight Doppler point & calculate center point of secondary ROI(s) and highlight
      - NOTE: can keep short history of previous points to guide identification of primary point when more than one option detected
  - Users can select the given center points (easy way to switch between 2+ possible ROIs)
    - Coords should propagate/recalculate with all continuing frames after in same mode (transverse/longitudinal)

## Action Items
- Redesign UI flow with new stages based on new edting specs
- Discuss new UI flow with Taha
- Detailed state diagrams
- UI prototypes
