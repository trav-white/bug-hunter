# Bug Hunter -- Deep QA Mascot & Visual System

The Bug Hunter is a pixel-art creature with a safari hat that narrates the QA process like Steve Irwin tracking wildlife through the bush, except the wildlife is code bugs. Every stage of the hunt gets its own terminal UI treatment -- Safari Trail, Mission Control, Threat Level, Trophy Case, and the Bug Hunter's running commentary.

**Credit line** (displayed on splash and final summary):
`Built by Trav White, Neighbourhood CO (www.nbh.co)`

---

## Visual Components

These are the building blocks. The **Composite Displays** section below shows how they combine at each step.

### 1. Safari Trail

A progress breadcrumb displayed at the top of EVERY stage (except splash). Shows linear flow through the hunt. Use `●` for completed, `◉` for current, `○` for upcoming. Display inside separator bars.

**Templates by current stage:**

```
HUNT stage:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
●━━━━━◉━━━━━○━━━━━○━━━━━○━━━━━○━━━━━○
SETUP  HUNT   FOUND  WRANGLE VERIFY LOOP   DONE
        ▲
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

FOUND stage:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
●━━━━━●━━━━━◉━━━━━○━━━━━○━━━━━○━━━━━○
SETUP  HUNT   FOUND  WRANGLE VERIFY LOOP   DONE
               ▲
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

WRANGLE stage:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
●━━━━━●━━━━━●━━━━━◉━━━━━○━━━━━○━━━━━○
SETUP  HUNT   FOUND  WRANGLE VERIFY LOOP   DONE
                      ▲
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

VERIFY stage:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
●━━━━━●━━━━━●━━━━━●━━━━━◉━━━━━○━━━━━○
SETUP  HUNT   FOUND  WRANGLE VERIFY LOOP   DONE
                             ▲
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

LOOP stage (Run 2+, append run count):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
●━━━━━●━━━━━●━━━━━●━━━━━●━━━━━◉━━━━━○   Run {N}/{max}
SETUP  HUNT   FOUND  WRANGLE VERIFY LOOP   DONE
                                    ▲
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

DONE stage:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
●━━━━━●━━━━━●━━━━━●━━━━━●━━━━━━━━━━━●
SETUP  HUNT   FOUND  WRANGLE VERIFY       DONE
                                           ▲
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

### 2. Mission Control

Agent dispatch board. Display when dispatching agents (Step 2). Show actual agents being sent based on the detected stack and scope. Use `◆` for deployed, `○` for standby, `✓` for returned clean, `✗` for returned with findings.

```
╔══════════════════════════════════════════════════════════════╗
║  MISSION CONTROL                                             ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  WAVE 1  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━     ║
║                                                              ║
║  ◆ Agent 1  Build & Tests         DEPLOYED  ▸▸▸              ║
║  ◆ Agent 2  Security & Auth       DEPLOYED  ▸▸▸              ║
║  ◆ Agent 4  Code Quality          DEPLOYED  ▸▸▸              ║
║  ◆ Agent 9  Dependencies          DEPLOYED  ▸▸▸              ║
║                                                              ║
║  WAVE 2  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━     ║
║                                                              ║
║  ○ Agent 5  API & Data            AWAITING WAVE 1            ║
║  ○ Agent 7  Flow & Integration    AWAITING WAVE 1            ║
║  ○ Agent 8  A11y & Performance    AWAITING WAVE 1            ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

Only show agents that are actually being dispatched for this session. Omit agents that don't apply to the detected stack.

When Wave 1 completes and Wave 2 dispatches, update the board:

```
╔══════════════════════════════════════════════════════════════╗
║  MISSION CONTROL                                             ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  WAVE 1  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  COMPLETE    ║
║                                                              ║
║  ✓ Agent 1  Build & Tests         CLEAN                      ║
║  ✗ Agent 2  Security & Auth       2 findings                 ║
║  ✗ Agent 4  Code Quality          1 finding                  ║
║  ✓ Agent 9  Dependencies          CLEAN                      ║
║                                                              ║
║  WAVE 2  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━     ║
║                                                              ║
║  ◆ Agent 5  API & Data            DEPLOYED  ▸▸▸              ║
║  ◆ Agent 7  Flow & Integration    DEPLOYED  ▸▸▸              ║
║  ◆ Agent 8  A11y & Performance    DEPLOYED  ▸▸▸              ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

---

### 3. Threat Level Meter

Visual severity indicator. Display after collecting results. Bar width: 32 characters.

```
Criteria and rendering:

Any P0:          THREAT LEVEL  ████████████████████████████████  EXTREME
P1s, no P0:      THREAT LEVEL  ████████████████████████░░░░░░░░  HIGH
P2s only:        THREAT LEVEL  ████████████████░░░░░░░░░░░░░░░░  MODERATE
P3s only:        THREAT LEVEL  ████████░░░░░░░░░░░░░░░░░░░░░░░░  LOW
No issues:       THREAT LEVEL  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  ALL CLEAR
```

---

### 4. Bug Trophy Case

Severity breakdown card with density bars. Display after collecting results. Bar length is proportional to count -- longest bar fills ~26 characters, others scale proportionally. Use different fill characters per severity. If a severity has 0 issues, show no bar.

```
╔══════════════════════════════════════════════════════════════╗
║  BUG TROPHY CASE -- Run {N}                                  ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  ████  P0  CRITICAL  ██████████████████████████   {count}    ║
║  ▓▓▓▓  P1  SERIOUS   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓        {count}       ║
║  ░░░░  P2  MODERATE  ░░░░░░░░░░░                 {count}     ║
║        P3  MINOR                                 {count}     ║
║                                                              ║
║  Total: {total} bugs spotted in the wild                     ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

---

### 5. Wrangling Progress

Fix progress display. Shows a progress bar and per-bug status. Update as each bug is fixed. Use `✓` for caught/fixed, `◆` for currently being wrangled, `○` for queued.

Bar width: 36 characters. Fill proportional to fixed/total.

```
  ████████████████████████░░░░░░░░░░░░  {pct}%  [{fixed}/{total} wrangled]

  ✓  P0  src/api/auth.ts:45          SQL injection       CAUGHT
  ✓  P1  src/api/deals.ts:89         Missing auth check  CAUGHT
  ✓  P1  src/hooks/useData.ts:34     Race condition      CAUGHT
  ◆  P2  src/pages/home.tsx:156      Missing error state  WRANGLING...
  ○  P2  src/styles/main.css:23      Container overflow   QUEUED
```

After all fixes complete:

```
  ████████████████████████████████████  100%  [{total}/{total} wrangled]

  ✓  P0  src/api/auth.ts:45          SQL injection       CAUGHT
  ✓  P1  src/api/deals.ts:89         Missing auth check  CAUGHT
  ✓  P1  src/hooks/useData.ts:34     Race condition      CAUGHT
  ✓  P2  src/pages/home.tsx:156      Missing error state  CAUGHT
  ✓  P2  src/styles/main.css:23      Container overflow   CAUGHT
```

---

### 6. Stats Dashboard

Enhanced stats with visual bars. Display at session end if HISTORY.md has entries. Bars are proportional -- the largest value gets the full 32-char bar, others scale. Also calculate and display **Capture Rate**.

```
╔══════════════════════════════════════════════════════════════╗
║  B U G   H U N T E R   S T A T S                             ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  Safari missions    {n}   {bar}                              ║
║  Bugs captured     {n}   {bar}                               ║
║  Clean sweeps       {n}   {bar}                              ║
║  Biggest haul       {n}   {bar}                              ║
║  Current streak     {n}   {bar}                              ║
║  Capture rate     {n}%   {bar}░                              ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

**Calculation:**
- `total_sessions` = number of HISTORY.md entries
- `total_fixed` = sum of fixed issues across all sessions
- `total_found` = sum of found issues across all sessions
- `sessions_passed` = count of PASSED sessions
- `max_issues_fixed` = highest single-session fix count
- `consecutive_pass` = current streak of consecutive PASSED sessions (0 if last was ESCALATED)
- `capture_rate` = `total_fixed / total_found * 100` (rounded to nearest int, cap at 100)

**Bar rendering:** For each stat, `bar_length = round(value / max_value * 32)`. The stat with the highest value gets 32 `█` chars, others scale down. Capture rate uses its own scale (percentage out of 32 chars, unfilled portion shown as `░`).

---

## Character States & Quotes

Each state has character art and a pool of Steve Irwin-style quotes. Pick ONE quote randomly per display. Never repeat the same quote within a session. Quotes with `{braces}` are templates -- fill in actual values.

### STATE: HUNTING

Display when sending agents out (Step 2). Character is scanning, eyes shifted right, legs splayed.

**Art:**
```
         ___
        /   \
    .----------.
    |    [] [] |
    |    __    |
    '----------'
    /||| || |||\
```

**Quotes:**
- "Crikey! Let's see what's lurking in this codebase..."
- "Easy now... nice and quiet... bugs can sense fear..."
- "Right, sending the trackers in. Surround 'em from all sides!"
- "Now THIS is what I call a proper bug safari!"
- "Shh... spreading out through the undergrowth of {scope}..."
- "These little rippers can't hide forever, I tell ya!"
- "Right, gather 'round! We're heading deep into {scope} territory!"
- "You can tell by the code smell... there's critters in here..."
- "I've seen some nasty bugs nest in {stack} before... stay sharp!"
- "These {file_count} files? That's prime bug habitat right there!"

---

### STATE: FOUND_P0

Display when results contain any P0 issues. Character is shocked -- round eyes, open mouth.

**Art:**
```
         ___
        / ! \
    .----------.
    | ()    () |
    |    <>    |
    '----------'
     ||| || |||
```

**Quotes:**
- "CRIKEY! That's a big one! P0 right in the wild!"
- "Strewth! Now THAT is a dangerous specimen right there!"
- "Whoa! Easy there! We've got a live P0 on our hands!"
- "Stone the crows! That's the deadliest bug I've seen all day!"
- "By crikey, she's ENORMOUS! A genuine P0 in its natural habitat!"
- "Blimey! Don't. Move. A. Muscle. That P0 can strike at any moment!"
- "CRIKEY! Look at the FANGS on that thing! Classic P0 behaviour!"

---

### STATE: FOUND_P1

Display when P1 issues found but no P0s. Character is alert -- angled eyes, focused.

**Art:**
```
         ___
        / ! \
    .----------.
    | >>    >> |
    |    __    |
    '----------'
     ||| || |||
```

**Quotes:**
- "Beauty! Got a P1 here -- she's a feisty one!"
- "Now THAT'S a beauty of a bug right there, mate!"
- "Crikey, look at the size of this P1!"
- "She's got some fight in her, this one. Gorgeous specimen!"
- "There she is! A wild P1! Look at her go!"
- "Now don't get too close -- P1s can still give you a nasty bite!"

---

### STATE: FOUND_MINOR

Display when only P2/P3 issues found. Character is calm -- normal eyes, flat mouth.

**Art:**
```
         ___
        /   \
    .----------.
    | []    [] |
    |    --    |
    '----------'
     ||| || |||
```

**Quotes:**
- "Little fellas here, nothing too dangerous..."
- "Aw, she's just a baby bug. No worries, mate!"
- "Found a shy one hiding in the corner there..."
- "Tiny little rippers, barely worth the fuss!"
- "Not the most dangerous critters, but we'll log 'em anyway!"
- "Couple of ankle-biters in here. Harmless, but let's clean up!"

---

### STATE: FOUND_CLEAN

Display when zero issues found. Character is relaxed -- sleepy eyes.

**Art:**
```
         ___
        / ~ \
    .----------.
    | --    -- |
    |    __    |
    '----------'
     ||| || |||
```

**Quotes:**
- "Crikey, this area's cleaner than a whistle!"
- "Nothing here, mate. Bugs must've heard us coming!"
- "Not a single critter! Someone's keeping this place tidy!"
- "All clear in this sector. Beautiful habitat, no pests!"
- "Well I'll be... not a single bug. Immaculate territory!"

---

### STATE: WRANGLING

Display when starting fixes (Step 5). Character is focused -- determined squint, legs braced.

**Art:**
```
         ___
        /   \
    .----------.
    | --    -- |
    |    __    |
    '----------'
     \|| || ||/
```

**Quotes:**
- "Right, let's wrangle this one! Hold still, ya little ripper..."
- "Easy does it... just gonna patch this up..."
- "No worries mate, I've handled worse than this before breakfast!"
- "Gotcha! Nice and easy... there we go, beauty!"
- "She's putting up a fight but we've got her! Almost... there!"
- "Now I'm gonna gently relocate this bug to the shadow realm..."
- "The trick is confidence. Bugs can smell hesitation!"

---

### STATE: LOOPING

Display when starting Run 2+. Character scanning again -- looking for survivors.

**Art:**
```
         ___
        / ? \
    .----------.
    |    [] [] |
    |    __    |
    '----------'
    /||| || |||\
```

**Quotes:**
- "Right, back in we go! There might be more hiding in the brush!"
- "Let's do another sweep -- can't be too careful in bug country!"
- "Crikey, I reckon there's a few more lurking in there..."
- "A good hunter always does a second pass. Let's move!"
- "Back into the thick of it! Follow me, stay close!"

---

### STATE: REGRESSION

Display when a previously-fixed bug reappears. Character is double-shocked.

**Art:**
```
         ___
        /!!!\
    .----------.
    | ()    () |
    |    !!    |
    '----------'
     ||| || |||
```

**Quotes:**
- "Crikey! That one came back from the dead! Thought we had her!"
- "She's BACK! That's one persistent little critter!"
- "Strewth! Didn't we already wrangle this one?! She's escaped!"
- "Well I'll be -- she's dug herself right back in! Crafty bug!"
- "CRIKEY! A regression! The most dangerous species of 'em all!"

---

### STATE: VICTORY

Display at session end when QA passes. Character celebrating -- happy eyes, legs raised.

**Art:**
```
         ___
        / * \
    .----------.
    | ^^    ^^ |
    |    __    |
    '----------'
     \|| || ||/
```

**Quotes:**
- "BEAUTY! Clean as a whistle! Not a bug in sight, mate!"
- "Crikey, what a hunt! Every last one of 'em caught and fixed!"
- "That's what I call a successful safari, right there!"
- "She's all clear! What a ripper of a result!"
- "Not a bug left standing! Absolute BEAUTY!"
- "And THAT is how it's done in bug country! Beautiful!"
- "What a day! The codebase is safe once again. Ripper!"

---

### STATE: ESCALATE

Display at session end when issues remain. Character confused -- question mark eyes.

**Art:**
```
         ___
        / ~ \
    .----------.
    | ??    ?? |
    |    ~~    |
    '----------'
     ||| || |||
```

**Quotes:**
- "These ones are too crafty for old mate here. Gonna need backup!"
- "Crikey... some of these bugs have SERIOUS fight in 'em!"
- "Right, some of these beauties need a specialist handler..."
- "I've done what I can -- some of these rippers need a human touch!"
- "Even Steve Irwin knew when to call for backup, mate!"
- "They've gone to ground. Gonna need someone to flush 'em out!"

---

## Composite Displays

These define exactly what to output at each step. Render ALL elements in a single code block per display unless noted otherwise.

### DISPLAY: Splash (after Step 0.11)

The first thing the user sees. Full framed card with character, title, session info, and opening quote.

```
╔══════════════════════════════════════════════════════════════╗
║                                                              ║
║                     ___                                      ║
║                    /   \                                     ║
║                    _____                                     ║
║                ___/     \___                                 ║
║               /             \                                ║
║              .---------------.                               ║
║              |   []     []   |                               ║
║              |      .__      |                               ║
║              '---------------'                               ║
║                |||  |||  |||                                 ║
║                                                              ║
║          D  E  E  P        Q  A                              ║
║          B  U  G     H  U  N  T  E  R                        ║
║                                                              ║
║  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━    ║
║                                                              ║
║  Mode:  {mode}  |  Files: {count}  |  Agents: {count}        ║
║  Stack: {detected stack summary}                             ║
║  Scope: {branch or area}                                     ║
║                                                              ║
║  "{selected HUNTING quote}"                                  ║
║                                                              ║
║  Built by Trav White, Neighbourhood CO (www.nbh.co)          ║
╚══════════════════════════════════════════════════════════════╝
```

Fill in `{mode}` (Lite/Standard/Full), `{count}` values, `{detected stack summary}` (e.g. "Next.js + TypeScript + Drizzle"), and `{branch or area}` from session setup data. Right-pad content lines inside the box to align with the right `║`.

---

### DISPLAY: Hunt (Step 2, before dispatching agents)

Safari Trail (HUNT stage) + Character with quote + Mission Control board.

Output the Safari Trail for HUNT stage, then the HUNTING character art with a quote beside it, then the Mission Control board showing which agents are being deployed in which wave.

---

### DISPLAY: Found (Step 3, after collecting results)

Safari Trail (FOUND stage) + Character (severity-appropriate state) with quote + Threat Level Meter + Bug Trophy Case.

If regressions detected, show the REGRESSION character and quote FIRST, then proceed with the severity-appropriate display.

The character art should appear with the quote beside it and the total bug count:

```
       ___
      / ! \
  .----------.
  | ()    () |    {total} bugs spotted in the wild!
  |    <>    |    "{selected quote}"
  '----------'
   ||| || |||
```

Then the Threat Level meter, then the Bug Trophy Case card.

Also show an **Updated Mission Control** board below the Trophy Case, showing which agents returned with findings (`✗`) vs clean (`✓`):

```
╔══════════════════════════════════════════════════════════════╗
║  FIELD REPORT                                                ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  ✓ Agent 1  Build & Tests         CLEAN                      ║
║  ✗ Agent 2  Security & Auth       2 findings                 ║
║  ✗ Agent 4  Code Quality          3 findings                 ║
║  ✓ Agent 9  Dependencies          CLEAN                      ║
║  ✗ Agent 5  API & Data            1 finding                  ║
║  ✓ Agent 8  A11y & Performance    CLEAN                      ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

---

### DISPLAY: Wrangle (Step 5, before starting fixes)

Safari Trail (WRANGLE stage) + Character with quote + Wrangling Progress tracker.

Show the WRANGLING character with the fix plan summary, then the progress bar at 0%, then the full bug list with all items as `○ QUEUED`.

As fixes are applied, mentally track progress. After ALL fixes complete, display the updated progress bar at its final percentage with `✓ CAUGHT` status on each fixed bug.

---

### DISPLAY: Verify (Step 5, after post-fix verification)

Safari Trail (VERIFY stage). No character art -- just show verification results:

```
  POST-FIX VERIFICATION
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Build:           ✓ PASSED
  Existing tests:  ✓ PASSED
  Regressions:     ✓ NONE DETECTED
```

If verification fails:
```
  POST-FIX VERIFICATION
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Build:           ✓ PASSED
  Existing tests:  ✗ 2 FAILURES
  Regressions:     ✗ 1 DETECTED
```

---

### DISPLAY: Loop (Step 6, when starting Run 2+)

Safari Trail (LOOP stage, with run counter) + LOOPING character with quote + Compact re-dispatch summary.

```
       ___
      / ? \
  .----------.
  |    [] [] |    Re-deploying {n} agents for Run {N}...
  |    __    |    "{selected LOOPING quote}"
  '----------'
  /||| || |||\

  Re-dispatching:
  ◆ Agent 1  Build & Tests         ALWAYS (regression gate)
  ◆ Agent 2  Security & Auth       P1 findings in Run {N-1}
  ◆ Agent 4  Code Quality          Scope touched by fixes
  ○ Agent 9  Dependencies          Skipped (clean + untouched)
```

---

### DISPLAY: Final -- Victory (Step 7, QA PASSED)

Safari Trail (DONE stage) + Full framed card with VICTORY character, results summary, quote, stats dashboard, and credit.

```
╔══════════════════════════════════════════════════════════════╗
║                                                              ║
║         ___                                                  ║
║        / * \                                                 ║
║    .----------.                                              ║
║    | ^^    ^^ |      Bug Hunter PASSED                       ║
║    |    __    |      {r} runs | {f} found | {x} fixed        ║
║    '----------'                                              ║
║     \|| || ||/       P0: 0  P1: 0  P2: 0 remaining           ║
║                                                              ║
║    "{selected VICTORY quote}"                                ║
║                                                              ║
╠══════════════════════════════════════════════════════════════╣
║  B U G   H U N T E R   S T A T S                             ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  Safari missions    {n}   {bar}                              ║
║  Bugs captured     {n}   {bar}                               ║
║  Clean sweeps       {n}   {bar}                              ║
║  Biggest haul       {n}   {bar}                              ║
║  Current streak     {n}   {bar}                              ║
║  Capture rate     {n}%   {bar}░                              ║
║                                                              ║
╠══════════════════════════════════════════════════════════════╣
║  Built by Trav White, Neighbourhood CO (www.nbh.co)          ║
╚══════════════════════════════════════════════════════════════╝
```

If no HISTORY.md exists yet (first session), omit the stats section -- just show character + results + quote + credit.

---

### DISPLAY: Final -- Escalate (Step 7, issues remain)

Same frame structure but with ESCALATE character and remaining issue summary:

```
╔══════════════════════════════════════════════════════════════╗
║                                                              ║
║         ___                                                  ║
║        / ~ \                                                 ║
║    .----------.                                              ║
║    | ??    ?? |      Bug Hunter ESCALATED                    ║
║    |    ~~    |      {r} runs | {f} found | {x} fixed        ║
║    '----------'                                              ║
║     ||| || |||       P0: {n}  P1: {n}  P2: {n} remaining     ║
║                                                              ║
║    "{selected ESCALATE quote}"                               ║
║                                                              ║
╠══════════════════════════════════════════════════════════════╣
║  REMAINING SPECIMENS                                         ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  {severity}  {file:line}  {description}          {status}    ║
║  {severity}  {file:line}  {description}          {status}    ║
║  ...                                                         ║
║                                                              ║
╠══════════════════════════════════════════════════════════════╣
║  B U G   H U N T E R   S T A T S                             ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  (same stats dashboard as Victory)                           ║
║                                                              ║
╠══════════════════════════════════════════════════════════════╣
║  Built by Trav White, Neighbourhood CO (www.nbh.co)          ║
╚══════════════════════════════════════════════════════════════╝
```

`{status}` for remaining bugs: `STUCK` (tried 2+ runs), `UNFIXED` (skipped/P3), `HUMAN REVIEW` (ambiguous fix).

---

## Display Integration Summary

| Step | Display | Components shown |
|------|---------|------------------|
| After 0.11 | **Splash** | Framed card: character + title + session info + quote + credit |
| Step 2 | **Hunt** | Safari Trail + HUNTING character + Mission Control |
| Step 3 | **Found** | Safari Trail + severity character + Threat Level + Trophy Case + Field Report |
| Step 5 start | **Wrangle** | Safari Trail + WRANGLING character + Progress tracker |
| Step 5 end | **Verify** | Safari Trail + Verification checklist |
| Step 6 | **Loop** | Safari Trail (with run counter) + LOOPING character + Re-dispatch summary |
| Step 7 pass | **Victory** | Safari Trail + Framed card: VICTORY character + results + stats + credit |
| Step 7 fail | **Escalate** | Safari Trail + Framed card: ESCALATE character + remaining + stats + credit |
