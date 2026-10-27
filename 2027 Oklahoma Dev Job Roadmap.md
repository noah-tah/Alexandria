# 2027 Oklahoma Dev Job Roadmap

Oct 27, 2026 · @Noah Tah

## Goal and ground rules

The target is a junior software developer job in Oklahoma (OKC or Tulsa area, or remote) during 2027, with TGMS as the centerpiece of your portfolio. Everything below serves three outputs: a finished, deployed TGMS; enough LeetCode to pass a junior technical screen; and interview skills to talk about both.

**The Oklahoma market, honestly**

- Oklahoma has about 6,880 software developer jobs; OKC's median pay is $122,390 and Tulsa's $108,730 (BLS, May 2025, via [TradeCareerPath](https://tradecareerpath.com/programs/online-software-development-degree/oklahoma/)). That's a thinner market than big tech hubs, so fewer openings and more weight on local connections.
- The same source notes employers weigh a portfolio of working code and passing technical interviews; certifications are optional. That is exactly what TGMS plus LeetCode covers.
- Entry-level roles do exist: Leidos posts entry-level developer roles in Lawton (Secret clearance required), and Tulsa has "Associate Software Engineer" postings ([iHire](https://ihire.com/t-software-developer-s-oklahoma-jobs.html)). A Tulsa direct-hire developer role listed $75,000–$85,000 ([Inceed](https://jobs.inceed.com/?p=53882)). Many other postings ask for 2–5 years, so plan to apply broadly, including remote roles.

**Ground rules**

- Consistency beats intensity. A sustainable 8–10 focused hours a week for a year beats 40 hours for three weeks and a crash.
- Sleep is part of the plan, not a reward. Learning consolidates during sleep.
- League stays at one night a week. Zero tends to snap back into a binge; one planned night doesn't.
- AI is the tutor, not the author. You type the code that ships.

**Open questions to fill in:** graduation date · TGMS tech stack · willing to commute/relocate within Oklahoma? · open to remote?

## The AI learning roles, mapped to coding

The video ([Nick Saraev](https://www.youtube.com/watch?v=FSXHk4hMrY8)) frames AI as a set of roles you assign it. YouTube only exposed the chapter list, not the transcript, so the descriptions below are built from the chapter titles. Add your own notes from watching in the last column.

| Role (video chapter)        | Use in coding                                        | Starter prompt                                                                                        | My notes from video |
| --------------------------- | ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------- |
| Interviewer                 | Before a chunk, find out what you already know       | "Ask me 5 questions to find what I know and don't about SQL joins before we start."                   |                     |
| Map maker                   | Break TGMS or a topic into an ordered list of chunks | "Map the concepts I need to build a login system, in learning order, smallest first."                 |                     |
| Explainer                   | Teach one concept at your level                      | "Explain dependency injection to someone who knows functions and classes. Use a table-games example." |                     |
| Reviewer                    | Review code you wrote by hand                        | "Review this function. Don't rewrite it; list problems by severity and ask me to fix them."           |                     |
| Socratic loop               | Guide you to the answer with questions               | "Don't give me code. Ask questions until I can write this myself."                                    |                     |
| Examiner                    | Test recall after a chunk                            | "Quiz me on what I built yesterday: 5 questions, no hints, grade me after."                           |                     |
| Listener / diagnostician    | You explain; AI finds the gaps                       | "I'll explain how my shift scheduler works. Point out anything wrong or vague."                       |                     |
| Sparring partner            | LeetCode and mock interviews                         | "Act as an interviewer. Give me an easy array problem and respond only to what I say."                |                     |
| Clerk                       | Keep notes and flashcards organized                  | "Turn today's session into 5 flashcards and a one-paragraph summary."                                 |                     |
| Right level                 | Keep difficulty just past comfortable                | "That was too easy. Give me the next harder version."                                                 |                     |
| Simulations / practice apps | Have AI build drills for you                         | "Make me 10 small exercises on string manipulation, increasing difficulty."                           |                     |
| Spaced repetition           | Revisit material at growing gaps                     | Re-quiz at 1 day, 3 days, 1 week, 1 month                                                             |                     |

**When AI hinders learning** (the video's last chapter): the moment you paste AI code you can't explain, you've stopped learning. If you couldn't rebuild it tomorrow, it doesn't count yet.

## The TGMS chunk loop

Every TGMS chunk goes through the same seven steps, one repo, two branches. A chunk should be small enough to rebuild in one or two sittings ("add a player and validate input", not "player tracking").

1. **Map** (Map maker): list the chunks for the next feature. Pick one.
2. **Diagnose** (Interviewer): AI asks what you already know about the chunk's concepts. Skip what you know.
3. **Learn** (Explainer, Socratic loop): concepts first, no code yet. End when you can describe the plan in your own words.
4. **Guided build** on `learn/<chunk>`: you type every line; AI guides and reviews (Reviewer). Commit often.
5. **Recall build** on `build/<chunk>`, at least a day later, AI closed. Write down every place you got stuck before looking anything up.
6. **Compare and examine**: `git diff learn/<chunk> build/<chunk>`, then AI quizzes you on the stuck points (Examiner, Listener). Merge the build branch into main once it works.
7. **Space it out**: AI re-quizzes you on the chunk after 3 days, 1 week and 1 month (Clerk keeps the list).

```
git checkout main && git checkout -b learn/add-player
# guided build, commit...
git checkout main && git checkout -b build/add-player
# recall build, commit...
git diff learn/add-player build/add-player
git checkout main && git merge build/add-player
```

The rule that keeps it honest: nothing lands on main that you couldn't explain in an interview.

## Roadmap: November 2026 to an offer in 2027

&#91;embedded content: 2027 roadmap · 4 phases, 4 gates\]

Don't move to the next phase until its gate is met; if a phase runs long, the later dates slide, not the gate. TGMS keeps its December 2026 target for the core, and Phase 2 polish covers anything that spills over.

## LeetCode: how much is enough

Aim for about 100–150 problems you can re-solve cold, starting with the LeetCode 75 list. That's enough for junior screens; quality of recall matters more than the count.

- Junior candidates on Glassdoor describe easy or easy-medium problems at Amazon, and one IBM candidate said knowing the LeetCode 75 was enough for a one-hour interview ([Glassdoor, IBM](https://www.glassdoor.co.nz/Interview/IBM-Interview-E354-RVW95557772.htm)). Another IBM candidate failed on dynamic programming they hadn't prepared for.
- A common benchmark for general technical interviews is 150–200 problems, mostly easy and medium ([DesignGurus](https://designgurus.io/answers/detail/how-many-leetcode-questions-should-i-solve)). Treat 150 as a ceiling for you, not a floor.
- Many Oklahoma employers (manufacturing, energy, government contractors) may lean on practical questions over puzzles. Check each company's Glassdoor interview page before you over-prepare.

**Patterns, in order:** arrays and hashing → two pointers → sliding window → stacks → binary search → linked lists → trees (DFS/BFS) → heaps → graphs → basic dynamic programming.

**How to practice each problem (with AI as sparring partner)**

1. 25 minutes alone, talking out loud as if in an interview.
2. Stuck? Ask for a hint ladder: "one small hint only." Never the full solution first.
3. After solving, ask the Reviewer for time/space complexity and a cleaner approach. Rewrite it yourself.
4. Log it. Re-solve from scratch after 3 days and again after 2 weeks. Only problems you pass on re-solve count toward the total.

| Problem | Pattern | First try | Re-solve day 3 | Re-solve week 2 |
| --- | --- | --- | --- | --- |
| Two Sum | Hashing |  |  |  |
|  |  |  |  |  |

## Interview skills

Your seven years dealing cards plus a project built for that industry is a story most junior candidates can't tell. Prepare three things.

**1. Behavioral stories (STAR: situation, task, action, result).** Write 5–6, each under two minutes spoken:

- Accuracy under pressure: running a game fast without payout errors
- Handling a difficult or upset player
- Following strict procedures and compliance (cash handling, game protection)
- Learning something hard while working nights and studying
- Why you built TGMS: a real problem you saw on the floor
- A mistake you made and what you changed

**2. The TGMS deep dive.** Be ready to spend 10 minutes on it:

- What it does and who it's for, in 30 seconds
- The architecture, drawn on a whiteboard from memory
- One design tradeoff you made and why
- The hardest bug you fixed and how you found it
- What you'd change with more time

The chunk loop (recall builds, examiner quizzes) is exactly the practice for this: you'll have rebuilt every part yourself.

**3. Mock interviews.** Use AI as the Interviewer once a week from Phase 3: one behavioral round and one coding problem, out loud. Record yourself every few weeks and watch for rambling and silent stretches. Add at least two mocks with real people (classmates, a career center, local tech meetups in OKC or Tulsa).

## Weekly template and this week's checklist

About 8–10 hours a week, placed around classes and shifts. Slot the sessions into whatever days fit; the weekend nights off are prime time for the long blocks.

| Session | Count per week | Length | What happens |
| --- | --- | --- | --- |
| TGMS chunk loop | 3 | 90 min | Steps 3–6 of the chunk loop |
| LeetCode | 3 | 30–45 min | One new problem or one re-solve |
| Review | 1 | 30 min | Spaced-repetition quizzes, update this doc |
| Interview prep | 1 (from Phase 3) | 45 min | Mock interview or STAR story practice |
| League | 1 night | Your call | Planned, guilt-free |
| Sleep | Every night | Full | Non-negotiable |

**This week**

- [ ] Watch the video and fill in "My notes from video" in the roles table
- [ ] Map TGMS into chunks with AI (Map maker) and pick the first one
- [ ] Run the first chunk through the loop on a `learn/` branch
- [ ] Solve 3 easy problems from the LeetCode 75 list and log them
- [ ] Answer the open questions in Goal and ground rules
- [ ] Plan this week's League night

## Sources

- [How I Learn Complex Skills & Difficult Subjects So Fast with AI — Nick Saraev](https://www.youtube.com/watch?v=FSXHk4hMrY8) (chapter list only)
- [Software Development in Oklahoma: Salary & Outlook — TradeCareerPath](https://tradecareerpath.com/programs/online-software-development-degree/oklahoma/)
- [Software Developer Jobs in Oklahoma — iHire](https://ihire.com/t-software-developer-s-oklahoma-jobs.html)
- [Software Developer, Tulsa — Inceed](https://jobs.inceed.com/?p=53882)
- [IBM Junior Software Developer interviews — Glassdoor](https://www.glassdoor.co.nz/Interview/IBM-Interview-E354-RVW95557772.htm)
- [Amazon Junior Software Developer interviews — Glassdoor](https://www.glassdoor.co.in/Interview/Amazon-Interview-E6036-RVW69707721.htm)
- [How many LeetCode questions should I solve? — DesignGurus](https://designgurus.io/answers/detail/how-many-leetcode-questions-should-i-solve)
