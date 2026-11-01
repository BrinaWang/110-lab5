# Lemon Clicker Bug Report

**Name: Brina**
**Tickets solved: 1, 2, 3** <!-- e.g. 1, 2, 3, 5, 6 (at least five) -->


## Ticket <3>: <The lemon only lands in four spots>

### Actual cause

<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->

**File / function: GameScreenView, randomizeLemonPosition()**

**What was wrong: the rounding was only rounding the random number instead of the random number multiplied by the bounds.**

### Fix
I changed the rounding parentheses to go around the entire random number multiplied by the bounds instead of just the random number so our result would be within (min, max) rather than (0, 1). the new lines are now: `const randomX = Math.round(Math.random() * (maxX - minX)) + minX;` and `const randomY = Math.round(Math.random() * (maxY - minY)) + minY;`

<!-- What did you change, and why does that change fix the problem? -->

### How did you find it? 

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**
The issue was with the lemon's random position so my initial instinct was to look at what method handled that position. Looking in the view screen led me to the randomizeLemonPosition() method, where it became apparent that the issue was how the random position was being calculated. 

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom: The lemon always lands in one of the four corners and is not truly random.** <!-- what you saw, e.g. text on screen, console error -->
2. **Buggy code: GameScreenView, randomizeLemonPosition() had the Math.round function only around Math.random instead of the entire full multiplied range.** <!-- the file, function and line where the trace ended -->

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->
I replayed the game and clicked the lemon at least ten times. It appeared in different places around the screen and not just the four corners. 
