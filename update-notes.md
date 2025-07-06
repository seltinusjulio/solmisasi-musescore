## Version 1.2 Update Notes

**Fixed Duration Handling:**
- Corrected duration calculation by accessing `parentChord.duration.ticks` instead of the unreliable `notes[i].chord.duration`
- Improved duration prefix/suffix logic for proper note length representation

**Enhanced Tie Notation:**
- Replaced generic dash symbols (`–`) with proper tie symbols (`~`)
- Reorganized tie handling with separate `tiePrefix` and `tieSuffix` variables for better code clarity
- Fixed tie symbol positioning in the final note representation

**Code Structure Improvements:**
- Better variable organization and naming conventions
- Cleaner separation of tie and duration handling logic
- More reliable access to chord properties through parent relationship

These changes primarily address the previously non-functional duration handling (marked as "BELUM BERFUNGSI" in v1.1) and provide more accurate solmisasi notation with proper tie symbols.

## Version 1.1 Update Notes

**New Features:**
- Added duration notation support with prefix/suffix indicators:
  - Whole note (4x): "..." suffix
  - Half note (2x): "." suffix  
  - Quarter note (1x): no modification
  - Eighth note (0.5x): "J" prefix
  - Sixteenth note (0.25x): "K" prefix
  - Thirty-second note (0.125x): "L" prefix
  - Other durations: "=" suffix
- Added tie notation support:
  - Tie forward: "–" suffix
  - Tie back: "–" prefix

**Technical Improvements:**
- Enhanced note representation with prefix/suffix system
- Improved chord duration handling with fallback to quarter note (480 ticks)
- Code optimization for better readability

**Known Issues:**
- Duration notation feature marked as "BELUM BERFUNGSI" (not yet functional) - requires further development for proper implementation