---
tags: [tgms, prompts]
source: https://claude.ai/artifact/1oESHgT6UWAuv6iuvE4JrL
---

# TGMS AI Prompts (AI-first)

Loop per slice, on branch `feat/<slice>`: **Spec → Plan → Generate → Walkthrough → Gate (questions + hand-made ticket) → Merge and keep.** Nothing merges until the gate passes.

| Step | Where | Prompt |
| --- | --- | --- |
| 1 Spec | Tutor chat | Tutor primer, Spec check |
| 2 Plan / 3 Generate | Claude Code | Build |
| 4 Walkthrough | Claude Code | Walkthrough |
| 5 Gate | Tutor chat (or Claude in the TGMS thread) | Interview gate, Change ticket, Break-it (optional) |
| 6 Keep | Tutor chat | Cards, Re-quiz (1 week, 1 month), Weekly whiteboard |

Keep the tutor chat separate from the coding agent. The CLAUDE.md for the repo is at the bottom.

## Tutor primer

```text
You are my tutor and mock interviewer. I'm building TGMS, a casino Table Games Management System, as my resume project for junior developer jobs. Stack: C#/ASP.NET Core (.NET 10), EF Core, PostgreSQL, React + TypeScript. I dealt table games for 7 years, so casino examples help.

I work AI-first: a coding agent writes the code, I direct and review it. Your job is to make sure I truly understand what was built before I merge it.

Today's slice: [SLICE]
Step: [SPEC CHECK / WALKTHROUGH HELP / GATE / RE-QUIZ]

Rules:
1. Ask one question at a time and wait for my answer.
2. When I ask you something, first ask what I think.
3. Be a fair but tough interviewer: don't accept vague answers like "it handles the data".
4. Explanations under 150 words, with a casino example when it helps.
5. At the end, list my weak spots.

Reply "Ready".
```

## Spec check

```text
SPEC CHECK: [SLICE]
Here's my spec, written by me:
[SPEC: what it does for the pit boss, acceptance criteria as "Given / When / Then", compliance rules it touches, what's out of scope]

Don't rewrite it. Find:
- Acceptance criteria that are vague or untestable
- Edge cases I missed (zero, negative, duplicates, two people at once, end of gaming day)
- Compliance rules from Title 31 or MICS that apply but aren't listed
Ask me to fix each one. Say "Spec ready" when it's solid.
```

Save the finished spec as `docs/specs/[slice].md` in the repo.

## Build (Claude Code)

```text
Build the slice in docs/specs/[slice].md on branch feat/[slice].
First, give me a plan only: files you'll add or change, data/migration changes, tests, and anything risky. For each decision, name the simpler alternative and why you didn't pick it.
Wait for my approval. After I approve, build it in small commits and follow CLAUDE.md.
```

Before approving: can I say why each file exists? Is anything a pattern I haven't seen? Ask about those first.

## Walkthrough (Claude Code)

```text
Walk me through this slice in data-flow order: start at the HTTP request (or the UI click) and follow it to the database and back.
One file at a time. For each file: what it does, the 2 or 3 lines that matter most, and why it's written that way.
Stop after each file and wait for my questions. Don't move on until I say "next".
At the end, show me how to run the tests and which test proves each acceptance criterion.
```

## Interview gate

```text
GATE: [SLICE]
Here's the PR walkthrough: [PASTE PR DESCRIPTION]
Here's the key code: [PASTE THE 2-3 MOST IMPORTANT FILES, OR THE DIFF]

Interview me on this slice like a technical interviewer at a company that builds casino software. Ask 6 to 8 questions, one at a time:
- 2 "walk me through": explain a flow or a file in my own words
- 2 "why": why this design and not an alternative
- 2 "what if": an edge case, a failure, or two users at once
- 1 domain question linking the code to Title 31 or MICS
- 1 "how would you change it to..." for a realistic new requirement
Don't hint. If my answer is vague, push once ("Be more specific"). Then grade it Solid, Shaky, or Missing.
After all questions: a table of grades, then for each Shaky or Missing, a 100-word explanation and one re-ask. I pass when every item is Solid.
```

## Change ticket (do it with Claude Code closed)

```text
TICKET: [SLICE]
Here's the code for this slice: [DIFF OR FILES]

Write me one small change request, like a real Jira ticket from a pit manager, that:
- touches 2 or 3 files of this slice
- I can finish in 20 to 30 minutes by hand
- has clear acceptance criteria
Don't tell me which files or how. When I paste my change, review it like a senior dev and tell me if it meets the criteria.
```

## Break-it (optional: slices 6, 9, 12, 14)

To Claude Code:

```text
On a new branch break/[SLICE], introduce one realistic bug into this slice, the kind a junior dev might write (off-by-one, wrong comparison, missing transaction, wrong gaming day). Don't tell me what or where. Make sure at least one existing test fails or could catch it. Then stop.
```

Find it with the failing test, the debugger, and logs. Explain the cause to the agent, then delete the branch.

## Cards

```text
CARDS: [SLICE]
My gate results: [GRADES TABLE + WEAK SPOTS]

Make 5 Anki cards from my Shaky and Missing items:
- One fact per card. Front is an interview-style question ("Why...?", "What happens if...?"). Back under 15 words.
- 1 card that connects this slice to an earlier one.
Output one card per line as: front | back | tgms::[SLICE]
Don't use the | character inside a card.
```

Import: Anki **File → Import**, separator Pipe, third field → Tags.

## Re-quiz (1 week and 1 month after merge)

```text
RE-QUIZ: [SLICE], [1-WEEK / 1-MONTH]
What it covered: [MUST-EXPLAIN LIST FROM THE SLICE TABLE]
Weak spots last time: [WEAK SPOTS]

5 questions, one at a time, no hints: 2 on weak spots, 2 applying it to a TGMS situation not built yet, 1 "describe this flow from memory". Grade at the end.
```

## Weekly whiteboard

```text
WHITEBOARD: I'm going to explain the TGMS architecture from memory as if I'm in a final-round interview.
So far I've built: [MERGED SLICES]
[MY EXPLANATION, OR A PHOTO OF MY DIAGRAM]

Act as the interviewer. Ask 3 follow-ups that dig into the weakest part of my explanation, one at a time. Then tell me what I got wrong or left out, and what a strong candidate would have said.
```

## CLAUDE.md (copy to the tgms repo root)

```markdown
# TGMS: rules for the coding agent

## Project
Table Games Management System for a casino pit. Portfolio project for a junior developer
(Noah) who must be able to explain every line in an interview. Domain: table games,
Title 31 (CTR, MTL), NIGC MICS / tribal TICS (fill and credit slips).

Stack: ASP.NET Core Web API (.NET 10, C#), EF Core 10 + PostgreSQL, ASP.NET Identity,
SignalR, React + TypeScript (Vite, TanStack Query), xUnit + Testcontainers, Vitest.
Layout: /api (backend), /api.Tests, /web (frontend), /docs (ERD, specs, decisions).

## How we work
1. Read the spec in docs/specs/<slice>.md first. If anything is unclear, ask before planning.
2. Propose a plan (files, data changes, tests, risks) and WAIT for approval before coding.
3. Work on branch feat/<slice>. Small commits with clear messages.
4. Prefer the simplest code a junior could explain. No clever abstractions, no new
   libraries without asking. Follow patterns already in the repo.
5. Write tests for every rule about money, slips, thresholds, and permissions.
6. Run `dotnet build`, `dotnet test`, and (for web) `npm test` before saying you're done.

## Non-negotiable domain rules
- Money is `decimal` in C# and `numeric(12,2)` in Postgres. Never double or float.
- CTR: currency transactions MORE THAN $10,000 per player per gaming day. Cash-in and
  cash-out are totaled separately, never netted. Only medium = Currency counts.
- Every money row is stamped with its GamingDay, not the calendar date.
- Issued slips, transactions, and audit rows are immutable: no update or delete endpoints.
  Corrections are void or reversing records.
- Slip serials are gapless per series: take the next number inside a DB transaction
  with a row lock. Never use a Postgres SEQUENCE for slip serials.
- Restricted slip copy is readable by the Accounting role only.
- Never log or return full SSNs. Encrypt at rest; show last 4 only.
- Never commit secrets. Use user-secrets locally and environment variables in production.

## When you finish a slice
Write the PR description as a walkthrough for Noah:
1. What the feature does, in 2 sentences.
2. Files in data-flow order (request -> controller -> service -> EF/DB -> response),
   one line each on its job.
3. Every design decision with the alternative you rejected and why.
4. New concepts used (e.g. "row lock", "partial unique index"), one line each.
5. Three questions an interviewer might ask about this slice.
```
