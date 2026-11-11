Learn v3.0.0
Author: AKX

Overview
Learn is a single-file browser application for studying term-and-definition decks. All data, settings, and session states are stored locally in browser localStorage under the key learn.local.v1. It has no external dependencies or network requirements.

v3.0.0 Changes

1. Study Modes
- Flashcards Mode: Displays cards one by one with a flip interaction. Includes two navigation sub-modes: standard sequential browsing (Previous/Next) and progress tracking (Still learning sets card level to 1; Know it sets card level to 2).
- Learn Mode: Adaptive rounds of up to 7 questions. Supports three format settings: Adaptive (Level 0 uses multiple choice, Level 1 uses written input), Written Only (all levels require typed answers), and Multiple Choice Only (all levels use up to 4 choices).
- Test Mode: Generates a single-page or sequential practice test from the deck. Users can configure question count, answer direction, and question types (True/False, Multiple Choice, Written). Calculates final percentage and lists missed items upon submission.

2. Grading and Input Controls
- Retype Requirement Toggle: Added a setting (requireRetype) to enable or disable mandatory answer retyping after an incorrect or skipped question.
- Quick Skip: Pressing Enter on an empty written input or Space during a multiple-choice question triggers the skip action instead of throwing a validation error.
- Hints: Pressing Alt+H in written mode reveals the first character of each word on the first press, and 40% of alphanumeric characters on the second press.
- Manual Override: Pressing Alt+R after an incorrect written answer marks the response as correct and increments the card level.
- Typo Tolerance: Written grading normalizes Unicode (NFKC), strips punctuation, ignores case, and accepts a Levenshtein distance of 1 on words longer than 5 characters.

3. Audio and Interface
- Web Audio API Synthesizer: Generates audio feedback for correct answers, incorrect answers, hints, round checkpoints, and deck completion using native browser oscillators. Can be toggled off in settings.
- Options Interface: Replaced native select elements with custom mode cards, segmented controls, and toggle switches.
- Version Tag: Added Made by AKX and v3.0.0 version identifiers to the sidebar and page footer.

4. Performance Changes
- Debounced Storage Writes: Draft input saving in written mode is debounced by 300ms to prevent synchronous localStorage serialization on every keystroke.
- Targeted DOM Updates: Hint reveals and option toggles update specific DOM nodes rather than re-rendering the full application shell.
- Batched Progress Bar Updates: DOM width reads and writes are separated into a single requestAnimationFrame pass to prevent layout thrashing.
- Compositor Animations: Removed backdrop-filter blur and replaced box-shadow/filter keyframe animations with transform and opacity transitions.

Keyboard Shortcuts
- 1 to 4: Select multiple-choice option
- Enter: Submit written answer, skip if input is empty, or advance to next question
- Space: Flip flashcard or skip multiple-choice question
- Alt + D: Skip current question (Don't know)
- Alt + H: Reveal letter hint in written mode
- Alt + R: Override incorrect grading in written mode
- Alt + S: Skip retyping correction
- Left / Right Arrows: Navigate or grade flashcards

Data Limits and Backups
- Maximum decks: 200
- Maximum cards per deck: 10,000 (50,000 total across all decks)
- Maximum field length: 120 characters for title, 500 for description, 5,000 per term or definition
- Import formats: Tab-separated or comma-separated text (Quizlet export format) and Learn v1 JSON backup files (up to 25 MB).
- <img width="1919" height="974" alt="image" src="https://github.com/user-attachments/assets/d7781335-7248-4c86-bb31-fe92a9c34e9c" />
