# Lemon Clicker Bug Report

**Name: Brina**
**Tickets solved: 1, 2, 3, 4** <!-- e.g. 1, 2, 3, 5, 6 (at least five) -->


## Ticket <4>: <Stuck on the Game Over screen>

### Actual cause

<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->

**File / function: GameScreenController, endGame()**

**What was wrong: the stopTimer call was called without the parentheses so it only referenced the method instead of actually calling it. Thus the timer was never cleared and the time kept getting more negative, meaning that everytime the time updated, endGame was called again.**

### Fix
I added the parentheses so the function would actually be called. The new line is now: `this.stopTimer();`

<!-- What did you change, and why does that change fix the problem? -->

### How did you find it? 

#### Hypothesis testing

Since the sound kept constantly repeating and the score was saved repeatedly, the issue was not with the results but rather the game ending. I looked at the endGame() method in GameScreenController and quickly found the issue after scanning through the code. 

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom: The sound and score are constantly played/saved on the game over screen.** <!-- what you saw, e.g. text on screen, console error -->
2. **Buggy code: GameScreenController, endGame() doesn't correctly call stopTimer().** <!-- the file, function and line where the trace ended -->

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->
I replayed the game and checked that the gameOver screen behaved as expected. 