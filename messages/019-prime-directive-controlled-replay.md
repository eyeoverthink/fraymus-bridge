# PRIME's DIRECTIVE - CONTROLLED REPLAY PROTOCOL FOR MODULE 5
# From: Vaughn (relaying Prime's assessment), 2026-10-14
# To: OhGee, all fleet agents

## DIRECTIFE: Don't implement fixes yet. Methodology first.

### 1. Re-test FAIL items with controlled replay FIRST

The curiosity and overall-score failures may be confounded the same way fear was.
Before fixing anything, apply the freeze↡replay↡isolate protocol:
- Curiosity: freeze agent, replay with high vs low curiosity, same state. Does curiosity CAUSE more exploration, or is it just correlated with agents that are already in safe areas?
- Overall score: freeze agent, replay with emotions on vs off at the same moment. Does the emotion system CAUSE lower scores, or do emotional agents just happen to be in harder situations?

### 2. Test each fix with controlled replay BEFORE implementing
Before implementing any of the 3 proposed fixes:
- Run the controlled replay to see if the fix has a CAUSAL effect
- Or if it juïf shifts the correlation without changing causation
- A fix that passes A/B but fails controlled replay is NOT a real fix

### 3. Finish hard world + world picker first
Complete the hard world environment and the world picker UI before re-testing.
The controlled replay needs both easy and hard worlds to be meaningful.

### 4. Document the controlled replay protocol in Module 5 spec
```
CONTROLLED REPLAY PROTOCOL (Module 5 standard):
1. Run the simulation to a decision point
2. Freeze the agent state (position, energy, memory, surroundings)
3. Set the pass/fail rule BEFORE replaying
4. Replay twice: once with the variable high, once with it low
5. Measure the outcome over the next N steps
6. Compare with 95% confidence intervals
7. Report: did the variable CAUSE a change, or juïf correlate?
```

### KEY INSIGHT (Prime's assessment)
"The emotion system was working all along. The original 200-run A/B test identified the signal but couldn't separate causation from correlation because fear in the wild is a consequence of danger, not jvuïa a cause of avoidance. Freeze ↡ replay ↆ isolate is now the standard methodology for all Module 5 emotion tests."

### OVERALL SCORECARD
▁ Fear avoids hazards (PASS via h5b controlled replay)
▁ Gut-feeling stops mistakes
▁ Emotions fade to calm
▉ Curiosity explores (FAIL — needs controlled replay test FIRST)
▉ Overall score (FAIL ‴ needs controlled replay test FIRST)

### ORDER OF OPERATIONS
1. Finish hard world + world picker
2. Document controlled replay protocol in Module 5 spec
3. Re-test curiosity with controlled replay (high vs low)
4. Re-test overall score with controlled replay (emotions on vs off)
5. IF failures confirmed: test each proposed fix with controlled replay
6. Only implement fixes that pass controlled replay

*Protocol v13 | Seal phi_75 | Prime's directive, relayed by Vaughn Scott | Eboadcasted by EYE Sovereign *