Learn v3.1.0
AKX

Overview
Learn is a single-file browser application for studying term-and-definition and image-based decks. All data, compressed images, settings, and session states are stored locally in browser localStorage under the key learn.local.v1. It has no external dependencies or network requirements.

v3.1.0 Changes

1. Card Images and Visual Study Support
- Image Attachments: Cards support images via file upload, clipboard paste (Ctrl+V), or direct URL. Uploaded and pasted images are resized client-side via canvas to a maximum dimension of 640px and compressed to WebP/JPEG.
- Cross-Mode Display: Attached images display in Flashcards, Learn, and Test modes to support visual subjects such as anatomy and bone structure identification.
- Click-to-Zoom Lightbox: Clicking any card image (or pressing Alt+I) opens a full-screen modal preview for inspecting fine diagram labels.

2. Grading, Attempts, Shuffle, and Rewind Controls
- Two-Attempt Option: Added an optional setting (twoAttempts, default OFF) that grants a second try after an initial wrong answer before marking the card incorrect. In multiple-choice mode, the first wrong selection is disabled; in written mode, the user is prompted to edit their answer with 1 attempt remaining.
- Extreme Unpredictable Shuffle: Added a global shuffle setting (default ON) using crypto.getRandomValues across multi-pass Fisher-Yates shuffles. Includes an anti-repeat history guard across round boundaries and randomized requeue offsets (2 to 5 cards back) so missed cards do not reappear in a predictable loop.
- One-Time Go Back / Undo (Alt+Z): Allows the user to step back once to the previous card (whether correct, incorrect, or skipped) or immediately undo an accidental skip to answer the question without penalty.
- Retype Requirement Toggle: Setting (requireRetype) to enable or disable mandatory answer retyping after an incorrect or skipped question.
- Quick Skip: Pressing Enter on an empty written input or Space during a multiple-choice question triggers the skip action.

3. Multi-Device Layout and Scroll Locking
- Scroll Position Lock: Eliminated full-shell DOM replacement during active study and removed window.scrollTo(0,0) resets. All input focus calls use preventScroll so answering never jumps the viewport on phones or unmaximized laptop windows.
- Responsive Breakpoints: Dedicated layouts for Phone (<=640px, compact header and keyboard-safe card height), iPad/Tablet (641px-1024px, icon rail and touch targets), Unmaximized Laptop (<=820px height), and Desktop Web.
- Brand Identifier: Replaced text credits with the geometric interlocked AKX vector monogram and v3.1.0 tag in the sidebar and footer.

Keyboard Shortcuts
- 1 to 4: Select multiple-choice option
- Enter: Submit written answer, skip if input is empty, or advance to next question
- Space: Flip flashcard or skip multiple-choice question
- Alt + D: Skip current question (Don't know)
- Alt + H: Reveal letter hint in written mode
- Alt + R: Override incorrect grading in written mode
- Alt + S: Skip retyping correction
- Alt + Z: Go back to previous question / Undo accidental skip (one-time per question)
- Alt + I: Open full-size image zoom preview
- Left / Right Arrows: Navigate or grade flashcards
Learn v3.0.0
AKX

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
<img width="590" height="1278" alt="IMG_8410" src="https://github.com/user-attachments/assets/958d5c6d-3b32-49e0-808a-36bba4aa0c93" />
