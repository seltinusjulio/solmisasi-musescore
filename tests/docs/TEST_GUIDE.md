# Test Guide: Solmisasi Plugin Fix Validation

## Overview
This guide explains how to use the generated test scores to validate Issue #2 fix and determine Issue #1 status.

## Test Files Created

### 1. `test_g_major.xml`
**Purpose:** Validate basic key signature support  
**Key Signature:** G Major (1 sharp: F#)  
**Content:** Ascending scale G-A-B-C-D-E-F#-G

**Expected Output (After Fix):**
```
G = 1
A = 2
B = 3
C = 4
D = 5
E = 6
F# = 7
G = 1
```

**Before Fix (Bug):**
```
G = 5 ❌ (wrong - should be 1)
A = 6 ❌ (wrong - should be 2)
B = 7 ❌ (wrong - should be 3)
C = 1 ❌ (wrong - should be 4)
```

---

### 2. `test_f_major.xml`
**Purpose:** Validate flat key signatures  
**Key Signature:** F Major (1 flat: Bb)  
**Content:** Ascending scale F-G-A-Bb-C-D-E-F

**Expected Output (After Fix):**
```
F = 1
G = 2
A = 3
Bb = 4
C = 5
D = 6
E = 7
F = 1
```

---

### 3. `test_chromatic_g_major.xml`
**Purpose:** Validate accidental marker rendering (Issue #1)  
**Key Signature:** G Major (1 sharp: F#)  
**Content:** Chromatic scale with all sharps and flats in proper positions

**Expected Output (After Fix):**
- All natural notes: correct scale degrees (1-7)
- Sharp accidentals: `/` symbol before scale degree (e.g., `/1` for G#)
- Flat accidentals: `\` symbol before scale degree (e.g., `\1` for Ab)
- Slash lines properly aligned on numbers (tests Issue #1 fix)

---

## How to Test

### Step 1: Import Test Score into MuseScore
1. Open MuseScore 3.x or 4.x
2. File → Open
3. Select one of the XML test files
4. Click Open

### Step 2: Set Up Font (Important for Issue #1 testing)
1. Format → Style
2. Navigate to: Text Styles → Staff
3. Set Font: "Parnumation 3.1" (if installed)
4. Apply and Close

### Step 3: Run the Plugin
1. Plugins → Composing/arranging tools → Solmisasi
2. Plugin should generate numerical notation above notes
3. Wait for completion (may take a few seconds)

### Step 4: Verify Results

#### For Issue #2 (Key Signature Support):
✅ **PASS if:**
- Notes display correct scale degrees for the key signature
- Example: In G major, B shows as "3" not "7"
- Example: In F major, Bb shows as "4" not as something else

❌ **FAIL if:**
- Notes still display as if key signature is C major
- Scale degrees don't match expected output above

#### For Issue #1 (Slash Rendering):
✅ **PASS if (using `test_chromatic_g_major.xml`):**
- Sharp accidentals (/) display cleanly on numbers
- Flat accidentals (\) display cleanly on numbers
- Slash lines appear properly overlaid, not misaligned
- No weird artifacts or double-rendering

❌ **FAIL if:**
- Slash characters appear misaligned or weird
- Numbers and slashes don't overlay properly
- Visual appearance is strange or unprofessional

### Step 5: Capture Results
1. Take screenshot of each test result
2. Document findings
3. Save results for GitHub issue update

---

## Quick Test Checklist

### Test 1: G Major Scale
- [ ] Imported successfully
- [ ] Plugin ran without errors
- [ ] B displays as "3" (not "7")
- [ ] F# displays as "7" (not as accidental on 4th)
- [ ] All scale degrees correct

### Test 2: F Major Scale
- [ ] Imported successfully
- [ ] Plugin ran without errors
- [ ] Bb displays as "4" (not as accidental)
- [ ] All scale degrees correct

### Test 3: Chromatic Notes in G Major
- [ ] Imported successfully
- [ ] Plugin ran without errors
- [ ] Sharp accidentals (/1, /2, etc.) display correctly
- [ ] Flat accidentals (\1, \2, etc.) display correctly
- [ ] Slash lines are properly aligned
- [ ] No weird rendering or misalignment

---

## Troubleshooting

### Plugin doesn't run
- Ensure plugin folder is in correct location
- Restart MuseScore
- Check console for error messages (View → Show Console)

### Font not available
- Parnumation 3.1 font must be installed on system
- Without it, accidental markers will show as plain text (/1, /2, etc.)
- Download from: https://gnibot.blogspot.com/2014/07/parnumation-3.html

### Strange output
- Try running plugin again
- Ensure no other plugins interfere
- Check that key signature is correctly set in MuseScore

### Slash lines still look weird
- This might indicate Issue #1 is separate from Issue #2
- Document exact appearance
- Check Parnumation font compatibility with MuseScore version

---

## Expected Duration

Each test should take approximately:
- **Test 1 & 2:** 2-3 minutes each (simple scale validation)
- **Test 3:** 3-5 minutes (detailed observation of accidentals)
- **Total:** ~15 minutes for complete validation

---

## Reporting Results

After testing, update GitHub issues with:

1. **Issue #2 Status:**
   - Does key signature support work? (Yes/No)
   - Which test cases passed/failed?
   - Any unexpected behavior?

2. **Issue #1 Status:**
   - Do slash lines render correctly? (Yes/No)
   - If no, describe the problem
   - Is it related to key signature fix or separate?

---

## Next Steps

Based on test results:

### If Both Tests Pass ✅
- Issue #2 is fixed
- Issue #1 is auto-resolved
- Ready for PR to main branch

### If Issue #2 Passes but Issue #1 Fails ⚠️
- Issue #2 fix is correct
- Issue #1 needs deeper investigation
- Create separate investigation branch for font rendering

### If Issue #2 Fails ❌
- Fix needs debugging
- Check error logs and stack trace
- May need to review key signature calculation logic

---

## Support
For questions or issues with testing, consult:
- test_plan.md (detailed test specifications)
- solmisasi.qml (plugin source code)
- GitHub issues (#1 and #2) for context
