---
title: "Worked Case Study"
nav_order: 8
---

[← Back to course home](index.md)

# Worked Case Study: One Small Task, Start to Finish

**Prerequisite:** Guides 1–4. This page doesn't teach new concepts — it shows how they chain together on a single, realistic task, since reading them in isolation can make each one feel like a separate skill rather than one workflow.

**The task:** add server-side email format validation to a signup form, with tests — a small, common, well-scoped feature you might find in any of this course's capstone projects.

The prompts and outputs below are **illustrative examples**, written to show the pattern — not a transcript from a real tool. Your actual output will differ. What matters is the *shape* of each step.

## Step 1 — Frame the requirement (Guide 1: Prompt Engineering)

Before touching code, we draft the acceptance criteria — a small SRS-style artifact — using the **Template-Fill pattern** from [Guide 1, Section 4](01-prompt-engineering.md#4-prompt-patterns-for-common-sdlc-tasks).

**Prompt:**
> Act as a requirements analyst. Here is our SRS acceptance-criteria template: [Given/When/Then format]. Draft acceptance criteria for: "the signup form must reject invalid email addresses." Cover the happy path and at least two edge cases. Return only the filled template, no extra commentary.

**Why this prompt works:** it has all five components from [Guide 1, Section 2](01-prompt-engineering.md#2-the-five-components-of-a-strong-prompt) — role (requirements analyst), context (our template), task (draft criteria for this one requirement), format (Given/When/Then, template only), and an implicit constraint (cover edge cases, not just the happy path).

**Illustrative output:**
```
Given a user on the signup form
When they submit an email without an "@" symbol
Then the form shows "Please enter a valid email address" and does not submit

Given a user on the signup form
When they submit a syntactically valid but disposable/blocked-domain email
Then [flag for team decision: allow or block? not specified in requirements]

Given a user on the signup form
When they submit a properly formatted email
Then the form accepts it and proceeds
```

Notice the model flagged an open question (disposable email domains) rather than silently deciding for us — a sign the prompt's constraints were doing their job. **This is exactly the kind of gap Guide 1, Section 6's rubric is designed to catch: read every output, don't just skim it.**

## Step 2 — Decide: workflow or agent? (Guide 2: AI Agents & Agentic Workflows)

Using the classification from [Guide 2, Section 2](02-ai-agents-agentic-workflows.md#2-workflows-vs-agents--an-important-distinction): the exact steps here (edit the validation function, add tests, run the suite) are knowable in advance for a task this small. This doesn't require an open-ended agent making unpredictable judgment calls — but it does benefit from a tool that can directly read and edit the actual codebase, which points us to Guide 4.

*(For a larger, less-defined task — "improve our form validation across the whole app" — the unpredictability of what you'd find in each file would make a fuller agentic approach, with more autonomy and more checkpoints, the better fit.)*

## Step 3 — Optional: a reusable review assistant (Guide 3: Custom GPTs & AI Assistants)

If this kind of validation-and-test task comes up repeatedly across your capstone project, it's worth building a small reusable assistant rather than rewriting this prompt from scratch each time — see [Guide 3, Section 3](03-custom-gpts-ai-assistants.md#3-when-a-custom-gpt-is-worth-building) for the fit test. For a one-off task like this single feature, a plain prompt is enough; we'd only build a custom GPT if we found ourselves repeating this exact pattern across many similar validation tasks.

## Step 4 — Implement with an agentic coding tool (Guide 4: Claude Code Basics)

Now we hand the acceptance criteria from Step 1 to an agentic coding tool, following the guidance from [Guide 4, Section 4](04-claude-code-basics.md#4-applying-prompt-engineering-to-an-agentic-coding-tool): state the goal, set boundaries, ask for a plan, verify independently.

**Prompt:**
> Add email format validation to the signup form based on these acceptance criteria: [paste Step 1 output, happy path + 2 edge cases]. Add unit tests covering all three cases in the existing test file for this module. Don't modify anything outside `src/forms/signup.js` and its test file. Propose your approach before making changes.

**Illustrative session flow:**
1. The tool reads `src/forms/signup.js` and its test file to understand existing conventions.
2. It proposes a plan: add a regex-based validation function, wire it into the existing submit handler, add three new test cases matching the acceptance criteria.
3. **You review the plan** — this is the checkpoint from [Guide 2, Section 5.3](02-ai-agents-agentic-workflows.md#53-ask-for-a-plan-before-execution). Say the plan looks right, but you notice it didn't address the flagged disposable-email question from Step 1 — you clarify: "skip disposable domain checking for now, just format validation," closing the gap before any code is written.
4. It shows the proposed diff. You review it the way you'd review a pull request, not skim a summary.
5. You approve. Files are updated.

## Step 5 — Verify independently (Guides 2 & 4)

Per [Guide 2, Section 5.4](02-ai-agents-agentic-workflows.md#54-verify-with-ground-truth-not-self-report) and [Guide 4, Section 6](04-claude-code-basics.md#6-what-claude-code-is-not-good-for-yet): don't trust "the tests pass" as a claim. Run the suite yourself.

```
npm test -- signup.test.js
```

If it passes: done, pending your own read of the diff for style/consistency. If it fails: paste the actual failure output back to the tool (see the [FAQ](06-faq-troubleshooting.md#-the-output-passed-my-read-through-but-failed-the-actual-tests)) rather than describing the failure from memory.

## Step 6 — Log it

Add one entry to your prompt log: the task, the tool(s) used at each step, and the outcome. Over a semester, this log becomes a record of how you actually used AI across your project — useful for your own reference and required for several graded exercises.

| Step | Tool | Prompt summary | Outcome |
|---|---|---|---|
| Requirements | Claude (chat) | Draft acceptance criteria for email validation | Accepted; flagged an open question we resolved manually |
| Implementation | Claude Code | Implement validation + tests per criteria, bounded to 2 files | Plan reviewed, one correction made before execution, diff approved |
| Verification | — (manual) | Ran `npm test` independently | Passed |

## What this case study is showing

The four guides aren't four separate skills you use in isolation — they're stages of **one** workflow: frame the problem clearly (Guide 1), decide how much autonomy the task needs (Guide 2), decide if it's worth making reusable (Guide 3), and execute with a tool that can touch real files while you stay the reviewer at every step (Guide 4). The habit that connects all four is the same one from [Guide 1, Section 6](01-prompt-engineering.md#6-evaluate-output-like-a-code-review): **read the output, don't just accept it.**

---
[← Previous: FAQ / Troubleshooting](06-faq-troubleshooting.md) · [Back to course home](index.md) · [Glossary →](glossary.md)
