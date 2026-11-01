# Lemon Clicker Bug Report

**Name: Brina**
**Tickets solved: 1, 2** <!-- e.g. 1, 2, 3, 5, 6 (at least five) -->


## Ticket <2>: <Best score always shows 0>

### Actual cause

<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->

**File / function: index.ts, app.get("/api/stats", (_req, res))**

**What was wrong: the logic for getting the best of all the entries was wrong. It had a < instead of a >**

### Fix
I changed the less than sign in the for loop to be a greater than sign instead. This fixes the issue because logically, the highest/greatest score is your best score. Thus, we should check that every entry is greater than best, so that we can update best accordingly. The new line is now: `if (entries[i].score > best) ...`

<!-- What did you change, and why does that change fix the problem? -->

### How did you find it? 

#### Hypothesis testing

**What hypothesis ultimately led you to identify the buggy code, and why?**
The best consistently showed 0, and there weren't any errors being thrown in the console, so I thought that it would be a logic-based error. I traced backwards and once I read index.ts and the corresponding app.get method, I saw that the logic for getting the best score would consistently give us 0 because it would always solve for the lowest score rather than the highest score. 

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom: The best score on the start screen is always 0 even though we have had a higher score in leaderboard.json.** <!-- what you saw, e.g. text on screen, console error -->
2. **Traced back to: MenuScreenView, the updateStats() method, which prints stats.best.** <!-- where that came from, e.g. a function, a request in the Network tab, a server log -->
3. **Traced back to: MenuScreenController, loadStatsFromServer(), which returns the JSON from the server.**
4. **Buggy code: index.ts, GET /api/stats handler was always calculating for the lowest score rather than the highest score. IT had a < instead of a >.** <!-- the file, function and line where the trace ended -->

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->
I reloaded the page with the leaderboard.json and saw that it displayed the correct best score. 
