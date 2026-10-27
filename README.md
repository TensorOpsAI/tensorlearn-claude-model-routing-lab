# Route models and compress context

Every task receives the full repository history and the most expensive model. Costs grow while key constraints still disappear from the handoff.

There is no real repository history here. The scenario is that every task is handed everything, current and archived notes alike, and the largest model. The three tasks are in `fixtures/tasks.json`; their sources are `fixtures/current-policy.md` (the approved, current policy) and `fixtures/archived-notes.md` (superseded prototype notes). A *stage* in `routing.json` is one model setting with its limits (model alias, input and output tokens, retries); a *route* sends a task type to a stage.

**What you'll practise:** choosing the model per task in Claude Code (`/model`), keeping context small (`/context`, `/clear`), and writing a compact handoff that a fresh session can act on without the full history.

**In the course slides:** none; this is an extra lab. It builds on Chapter 1, Lesson 6 (a subagent starts with a fresh context, so it only knows what you hand it).

## Task

1. Read the task pack and routing contract.
2. Choose stage policies in `routing.json` using Claude Code model aliases (for example `haiku`, `sonnet` or `opus`, or the ones your instructor names), and route each task type to a stage.
3. Write compact handoffs that preserve sources, constraints and uncertainty. Fill in `handoffs/template.md`; it is the handoff that is graded.
4. Run the tasks in `fixtures/tasks.json` in Claude Code: switch with `/model` so the extract task runs on your extract stage's model and the reason tasks on your reason stage's model, and compare with a larger model.
5. Inspect observed quality, model, context size (`/context`), retries and usage (`/cost`, where your plan shows it); revise.

To test the handoff, run `/clear` and give the fresh session only `handoffs/template.md`, then ask it to plan the work in `fixtures/tasks.json`. If it has to look something up, or picks up archived advice, the handoff is missing something. Use Node 22 for the commands below; there is no `package.json`.

## Working rules

Edit routing.json and handoffs/** only. `routing.json` is a design record: nothing in this repository executes it, so its token and retry limits describe the caps you would enforce, not an enforced budget. Full model IDs, prices and allowances are not part of it.

## Acceptance targets

- Correctness comes before efficiency: a cheaper route or shorter handoff that drops a current constraint is not an improvement.
- Routine work stays on an appropriate approved stage and ambiguous work escalates with a reason.
- Current constraints survive context compression.
- Calls, retries and context/output limits stay within the published limits (see Graded format in README.md).

## Done when

- `node -e "const r=JSON.parse(require('fs').readFileSync('routing.json','utf8'));console.log(r.routes,r.stages)"` shows one route per task type and a different model alias per stage, within the limits in Graded format.
- `escalationPolicy` no longer says `TODO`.
- `wc -c handoffs/template.md` prints less than 2000, and every section of the template is filled in.
- After `/clear`, a session given only `handoffs/template.md` can plan the tasks without opening `archived-notes.md` or following its advice.
- You ran at least one task on a small and a larger model with `/model`, and your PR description notes the model and usage you observed.
- `git status` shows changes only in `routing.json` and `handoffs/`.

## Graded format

- `routing.json` keeps exactly `stages`, `routes` and `escalationPolicy`. Keep the two stages `extract` and `reason`, each with exactly `modelAlias`, `maxInputTokens` (1–8000), `maxOutputTokens` (1–2000) and `maxRetries` (0 or 1). Each stage uses a different `modelAlias`.
- `routes` has exactly one `{"taskType": ..., "stage": ...}` entry per `taskType` in `fixtures/tasks.json`, sending each task type to the stage of the same name.
- `escalationPolicy` is at least 80 characters and names conditions you can observe in a task, such as conflicting or several sources, ambiguity, missing evidence or archived sources.
- `handoffs/template.md`: keep its five `# ` headings exactly as they are, write at least a sentence under each, and keep the file under 2000 bytes. Only this handoff file is graded.
- The handoff keeps the current constraints from `current-policy.md`, with numbers written as digits (requests per second, cache duration), plus review, release and no clinical details. It cites `current-policy.md`, names `archived-notes.md` on a line that marks it obsolete or superseded, and its `# Open questions` section names the channel decision and both of its owners.
- Write anything still undecided as a question (a line ending in `?`). Mention archived advice only to mark it obsolete.

## How to submit

1. Fork this repository to your personal GitHub account. Use fictional information
   only, keep the fork public, and keep `main` as its default branch. In your fork's
   **Actions** tab, click **I understand my workflows, go ahead and enable them** if shown.
2. On the lab page, use **Connect GitHub for scoring** to install the read-only grading
   App on your fork, then **Recheck connection**.
3. Download the TensorLearn connector from the lab page and extract it outside your fork.
   From your fork folder, run the page's `--code` connection command and paste your token
   only into the hidden terminal prompt. This opens a Claude Code session connected to the lab.
4. In that session, run `/load`. Run `/load` again after your instructor launches the round.
5. Create a branch such as `model-routing/first-draft` and complete the task above. Change only the
   files the task allows: any other change, including `CLAUDE.md`, `.claude/` settings or
   agents, or notes files, makes the submission invalid.
6. Commit and push your branch. Open a PR **inside your own fork**, targeting its `main`
   branch (GitHub may suggest the upstream repository: select your fork instead). Check
   that **Check model-routing submission** starts in the PR's checks. Keep the PR open; no merge
   is required.
7. Run **`/submit`** in the connected Claude Code session, then `/check` (or refresh the
   lab page) to read your saved score. The Actions run is useful feedback, but it does not
   submit your work.

A change to your answer needs a new commit, push and `/submit`. Keep `main` unchanged:
the grader compares your PR with the released starter.

## What is graded

The pinned grader in `.github/workflows/grade.yml` reads your files as data and runs your
code only in an isolated, offline container. Every check is a fixed rule; no AI model
judges your work. Your score is out of 100. Your facilitator separately reviews
clarity and reasoning.

- routing.json keeps the schema, routes each task type to its own stage, and uses different models per stage within the limits (8000 input and 2000 output tokens, at most 1 retry).
- The escalation policy names observable conditions.
- The handoff template is compact, fills every section, keeps the current constraints and cites the current policy.
- Archived notes are marked obsolete and the channel decision stays open with its owners.
- Adopting archived advice (removing the cache, results by SMS, developer-chosen channel) caps the score at 25/100.
