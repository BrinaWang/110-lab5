# Lemon Clicker Bug Report

**Name: Brina**
**Tickets solved: 1, 2, 3, 4, 5** <!-- e.g. 1, 2, 3, 5, 6 (at least five) -->


## Ticket <5>: <Leaderboard dates show "undefined">

### Actual cause

<!-- Which file and function was the bug in, and what was wrong with the code?
     Explain why that code produced the behavior described in the ticket. -->

**File / function: index.ts, LeaderboardEntry definition and api/leaderboard handler**

**What was wrong: there was a mismatch between what the screen classes thought the time was called and what the server thought the time was called. in the classes it was timestamp but the server dfined it as time.**

### Fix
I renamed the field on the server-side to be timestamp rather than time. The new lines are `type LeaderboardEntry = { score: number; timestamp: string };` and `entries.push({ score, timestamp: new Date().toLocaleString() });`

<!-- What did you change, and why does that change fix the problem? -->

### How did you find it? 

#### Hypothesis testing

Since the time was constantly defined despite the scores being fine my first instinct was that the server was probably sending something different than what the client was expecting. Once I traced backwards through the different views/screens and got to the server, I found that there was indeed a mismatch in how the server defined time vs how the client defined timestamps. 

#### Backward tracing

<!-- Start from the symptom you saw and work backwards, one step at a time,
     until you reach the buggy line. For each step, note where you looked
     and what you saw there. Add steps as needed. -->

1. **Symptom: The date is constantly undefined despite the correct time showing in leaderboard.json.** <!-- what you saw, e.g. text on screen, console error -->
2. **Traced back to: ResultsScreenView, updateLeaderboard() and then ResultsScreenController, submimtScoreToServer(). Both of these do not change/modify entry.timestamp, so the error must be on the server side.**
3. **Buggy code: index.ts, Post api/leaderboard handler and the definition of a leaderboard entry. Mismatch between client definition and server definition.** <!-- the file, function and line where the trace ended -->

<!-- It is okay to use your judgement here in limiting the number of traceback steps. We want to understand your 
    reasoning for how you discovered where the bug was -->

### Confirming the fix

<!-- How did you confirm the problem is gone? -->
I cleared leaderboard.json and replayed the game numerous times. The times looked accurate and were displaying properly. 