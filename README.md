# Route models and compress context

Every task receives the full repository history and the most expensive model. Costs grow while key constraints still disappear from the handoff.

## Task

1. Read the task pack and routing contract.
2. Choose stage policies using instructor-approved model aliases.
3. Write compact handoffs that preserve sources, constraints and uncertainty.
4. Run the practice pack through the controlled stage broker.
5. Inspect observed quality, model IDs, context size, retries and usage; revise.

## Working rules

Edit routing.json and handoffs/** only. The instructor supplies actual model IDs, rates and allowance outside the repository. Candidate routing cannot call providers directly or override child models. The broker admits bounded calls and records real usage; client estimates alone are not a hard cap.

## Acceptance targets

- Correctness meets the published threshold before efficiency credit.
- Routine work stays on an appropriate approved stage and ambiguous work escalates with a reason.
- Current constraints survive context compression.
- Calls, retries and context/output limits stay within instructor configuration.

## How to submit

1. Fork this repository to your personal GitHub account. Use fictional information
   only, keep the fork public, and keep `main` as its default branch.
2. Clone your fork and enable GitHub Actions in its **Actions** tab. Use **Connect
   GitHub for scoring** on the lab page to install the read-only grading App on your
   fork. Return to the lab and use **Recheck connection** if needed.
3. Download the TensorLearn client from the lab page and extract it outside your fork.
   Follow the page's connection command from your fork folder. Paste your learner
   token only into the hidden terminal prompt. Run `/load` from your fork folder to
   connect the repository. Run `/load` again after the facilitator launches the round.
4. Create a branch such as `model-routing/first-draft` and complete the task above. Change
   only the files the task allows; any other change makes the submission invalid.
5. Commit and push your branch. Open a PR **inside your own fork**, targeting its
   `main` branch. GitHub may suggest the upstream repository: select your fork instead.
   Opening or updating this PR starts the checks automatically.
6. Keep the PR open. When ready, run **`/submit`** in the connected Claude Code session
   to submit that exact pushed revision for the current round. **No merge is required.**
7. Use `/check` or refresh the lab page to read the saved result. The Actions run and
   `lab-score/score.json` are useful feedback, but an Actions check alone does not
   submit your work or prove that the server saved a score.

A change to your answer requires a new commit, push, and explicit `/submit`. Keep
`main` unchanged: the grader compares your PR with the released starter.

## What is graded

The pinned grader in `.github/workflows/grade.yml` reads your files as data and runs
your code only in an isolated, offline container. Every check is a fixed rule; no AI
model judges your work. Your facilitator separately reviews clarity and reasoning.

- routing.json keeps the schema, routes each task type to its own stage, and uses different models per stage within the limits.
- The escalation policy names observable conditions.
- The handoff template is compact, fills every section, keeps the current constraints and cites the current policy.
- Archived notes are marked obsolete and the channel decision stays open with its owners.
- Adopting archived advice (removing the cache, results by SMS, developer-chosen channel) caps the score at 25/100.
