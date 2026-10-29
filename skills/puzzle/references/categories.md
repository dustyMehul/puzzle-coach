# Categories and levels

Use this when picking a puzzle. The families below are starting points, not a fixed bank. Levels are a guide: judge the puzzle you actually pose, including its numbers. Changing the numbers in a well-known puzzle is fine, as long as you solve the new version yourself first and are sure of the answer.

If the user says they already know a puzzle, thank them for saying so, mark it `abandoned` with no level change, and pick another.

## What a level means
| Level | Feel | Typical shape |
|---|---|---|
| 1–3 | easy | one step, the trick is visible |
| 4–5 | medium | one key idea, a couple of steps |
| 6–7 | medium-hard | a key idea plus a careful setup (a recursion, a case split) |
| 8–9 | hard | a non-obvious idea, and the answer needs an argument, not just a construction |
| 10 | very hard | several ideas chained, or a known hard classic that needs a general rule or proof |

## Built-in categories
For each: what it tests, then puzzle families by level band.

### Logic and deduction
Tests: turning statements into eliminations, reasoning about what others know.
- 4–5: knights and knaves (two people), two doors and two guards, three switches and a bulb in another room
- 6–7: hats in a line (two colours, guarantee all but one), three people with hats seeing each other
- 8–9: Cheryl's birthday, muddy children, blue-eyed islanders (small numbers)
- 10: blue-eyed islanders (general case), the sum and product puzzle, the three gods puzzle

### Probability and expected value
Tests: setting up the sample space, conditioning, first-step recursions, symmetry.
- 4–5: Monty Hall, two-child problems, the birthday problem
- 6–7: expected flips to get two heads in a row, first to roll a six wins, expected rolls to see all six faces
- 8–9: the lost airplane boarding pass, broken stick into a triangle, HTH vs HTT waiting times
- 10: the 100 prisoners and 100 boxes, Penney's game with a full argument

### Number and counting
Tests: invariants, pairing, parity, recursion, binary.
- 4–5: 100 lockers, trailing zeros of a factorial, total handshakes in a room
- 6–7: poisoned wine with few testers, clock hands overlapping in a day, the mutilated chessboard
- 8–9: party handshakes with couples (all different answers), the sword circle (every second person)
- 10: the sword circle with the general rule and proof, counting problems that need a bijection

### Weighing and optimisation
Tests: information per step, case splits, worst-case thinking.
- 4–5: fake-coin bags with one weighing on a scale, 9 balls and 2 weighings, burning ropes to measure 45 minutes
- 6–7: bridge and torch (four people), two eggs and 100 floors, water jugs
- 8–9: 12 coins with 3 weighings (heavier or lighter unknown), bridge and torch (five people), camel and bananas
- 10: 13 coins with 3 weighings and one extra genuine coin, the jeep problem

### Strategy and game theory
Tests: backward induction, symmetry strategies, winning and losing positions.
- 4–5: take 1–3 matches, last one loses; race to 100 adding 1–10
- 6–7: pirate gold (five pirates), simple Nim
- 8–9: coins on a round table, Nim with several heaps (with the XOR rule explained)
- 10: pirate gold with more pirates than coins

### Lateral thinking
Tests: reframing the problem so it becomes easy.
- 4–5: light switches with heat, the monk walking up and down a mountain on two days
- 6–7: the fly between two trains, 100 coins with 10 heads up split blindfolded into two equal-heads piles
- 8–9: ants on a stick (worst-case time), ants on a stick (where a marked ant ends up)
- 10: ants on a circle

### Estimation
Tests: structured breakdown, stated assumptions, sanity checks. Scored on method and a figure within ~3× of a reasonable reference, not on an exact answer.
- 4–5: piano tuners in a big city, coffee cups sold in a city per day
- 6–7: golf balls in a plane, petrol stations in a country
- 8–9: market size for a product, revenue of a large business, with two independent cross-checks
- 10: the same with a second method and a reconciliation of the two

## Free-text topics
Users can add their own topics in `categories` (for example "SQL logic", "geometry", "Bayes"). Pick a puzzle that genuinely fits, has one definite checkable answer, and matches the level guide above. If nothing honest fits the topic at that level, say so and offer the nearest built-in category.
