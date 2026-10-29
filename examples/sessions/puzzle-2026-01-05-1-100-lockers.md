# Puzzle 2026-01-05 #1: 100 lockers

Hub: [puzzles](../puzzles.md)

- Status: closed
- Level: 5 · Category: number and counting
- Started: 09:12 · Ended: 09:24
- Hints: none
- Result: Solved
- Answer checked: yes (listed the squares up to 100 and counted them)
- Level change: 5 → 6

## Puzzle
A corridor has 100 closed lockers, numbered 1 to 100. 100 students walk past in turn. Student k toggles every locker whose number is a multiple of k (opens it if closed, closes it if open). After all 100 students have passed, how many lockers are open?

## Thinking trail
- 09:14 Tried lockers 1–10 by hand; noticed 1, 4 and 9 stay open.
- 09:19 Linked toggles to divisors; divisors come in pairs except for square roots.
- 09:23 Final answer: 10 (the perfect squares).

## Solution
Locker n is toggled once for each divisor of n. Divisors pair up (d with n/d), so the count is odd only when n is a perfect square. There are 10 squares up to 100, so **10 lockers** are open.

## Review
Solved, no hints. Small cases first, then the divisor-pairing argument, said aloud. Interviewer read: clean and well explained.
