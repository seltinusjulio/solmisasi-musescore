# Test Plan: Key Signature Fix Validation

## Objective
Validate that Issue #2 (key signature bug) is fixed and determine if Issue #1 (slash line rendering) is auto-resolved.

## Test Scenarios

### Test Case 1: C Major (Control/Baseline)
**Key Signature:** C Major (no sharps/flats)
**Notes:** C D E F G A B C

**Expected Output (Scale Degrees):**
- C = 1
- D = 2
- E = 3
- F = 4
- G = 5
- A = 6
- B = 7

**Note:** This should work the same before and after fix (baseline).

---

### Test Case 2: G Major (+1 Sharp)
**Key Signature:** G Major (F#)
**Notes:** G A B C D E F# G

**Expected Output (Scale Degrees):**
- G = 1 (tonic)
- A = 2
- B = 3
- C = 4
- D = 5
- E = 6
- F# = 7 (natural in key)
- G = 1 (octave)

**Before Fix (BUG):**
- G = 5 ❌ (calculated as if C is tonic)
- A = 6 ❌
- B = 7 ❌
- C = 1 ❌
- D = 2 ❌
- E = 3 ❌
- F# = /4 ❌ (wrong scale degree)

**After Fix (CORRECT):**
- G = 1 ✅
- A = 2 ✅
- B = 3 ✅
- C = 4 ✅
- D = 5 ✅
- E = 6 ✅
- F# = 7 ✅

---

### Test Case 3: D Major (+2 Sharps)
**Key Signature:** D Major (F#, C#)
**Notes:** D E F# G A B C# D

**Expected Output (Scale Degrees):**
- D = 1
- E = 2
- F# = 3
- G = 4
- A = 5
- B = 6
- C# = 7
- D = 1

---

### Test Case 4: F Major (-1 Flat)
**Key Signature:** F Major (Bb)
**Notes:** F G A Bb C D E F

**Expected Output (Scale Degrees):**
- F = 1
- G = 2
- A = 3
- Bb = 4 (natural in key, but shown as flat for notation)
- C = 5
- D = 6
- E = 7
- F = 1

---

### Test Case 5: Bb Major (-2 Flats)
**Key Signature:** Bb Major (Bb, Eb)
**Notes:** Bb C D Eb F G A Bb

**Expected Output (Scale Degrees):**
- Bb = 1
- C = 2
- D = 3
- Eb = 4
- F = 5
- G = 6
- A = 7
- Bb = 1

---

### Test Case 6: Chromatic Notes in G Major (Issue #1 - Slash Rendering)
**Key Signature:** G Major (F#)
**Test Notes with Accidentals:**

| Note | Scale Degree | Type | Display Format | Expected Output |
|------|--------------|------|---|---|
| G | 1 | Natural | 1 | 1 |
| G# | 1.5 | Sharp | /1 | /1 |
| Ab | 1.5 | Flat | \1 | \1 |
| A | 2 | Natural | 2 | 2 |
| A# | 2.5 | Sharp | /2 | /2 |
| Bb | 2.5 | Flat | \2 | \2 |
| B | 3 | Natural | 3 | 3 |
| C | 4 | Natural | 4 | 4 |
| C# | 4.5 | Sharp | /4 | /4 |
| D | 5 | Natural | 5 | 5 |
| D# | 5.5 | Sharp | /5 | /5 |
| Eb | 5.5 | Flat | \5 | \5 |
| E | 6 | Natural | 6 | 6 |
| E# | 6.5 | Sharp | /6 | /6 |
| F | 6.5 | Flat | \6 | \6 |
| F# | 7 | Natural (in key) | 7 | 7 |
| Gb | 7 | Enharmonic | \7 | \7 |

**Note:** This test case validates both the scale degree AND the accidental marker placement. If Issue #1 was caused by Issue #2, the slash lines should now appear correctly aligned.

---

## Validation Checklist

### Issue #2 Validation (Key Signature Support)
- [ ] Test Case 1 (C Major) - passes
- [ ] Test Case 2 (G Major) - B shows as 3, not 7
- [ ] Test Case 3 (D Major) - F# shows as 3, not as sharp on some degree
- [ ] Test Case 4 (F Major) - Bb shows as 4, not as something else
- [ ] Test Case 5 (Bb Major) - All notes display correct scale degrees

### Issue #1 Validation (Slash Line Rendering)
- [ ] Test Case 6 - All sharp accidentals (/) display correctly
- [ ] Test Case 6 - All flat accidentals (\) display correctly
- [ ] Slash lines appear properly aligned with numbers
- [ ] No weird overlapping or misalignment
- [ ] Works with Parnumation 3.1 font

---

## Test Procedure

1. **Create test scores** in MuseScore for each test case
2. **Set text style** to Parnumation 3.1 font (if available)
3. **Run the plugin** on each score
4. **Capture output** (screenshot or visual inspection)
5. **Compare with expected output** from test cases above
6. **Document findings** in GitHub issues

---

## Expected Outcomes

### If Issue #2 Fix is Successful:
✅ All scale degrees will be correct relative to key signature
✅ Chromatic notes will show correct accidentals (/ and \)

### If Issue #1 is Auto-Resolved:
✅ Slash lines will display properly with Parnumation font
✅ No weird alignment or overlapping
✅ Visual appearance matches expected notation

### If Issue #1 Persists:
⚠️ Slash lines still display incorrectly despite fix #2
⚠️ Needs deeper investigation into Parnumation font compatibility
⚠️ May be separate rendering bug in MuseScore

---

## Tools Needed

- MuseScore 3.x or 4.x
- Parnumation 3.1 font (installed on system)
- Test scores (will be provided as MusicXML or manual creation guide)
- Plugin: solmisasi.qml (from this branch)
