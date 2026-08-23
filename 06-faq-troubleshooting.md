---
title: "FAQ / Troubleshooting"
nav_order: 7
---

[← Back to course home](index.md)

# FAQ / Troubleshooting

Common failure modes you'll hit while using AI tools for coursework, what's actually happening, and what to do about it. Organized by symptom — find what you're seeing, not a topic name.

## "It gave me a confident, detailed, completely wrong answer"

**What's happening:** This is a **hallucination** (see [Glossary](glossary.md#hallucination)) — the model generated something plausible-sounding rather than something true, and nothing in its tone signals the difference. Models don't have a built-in "I'm not sure" flag; confident phrasing is not evidence of correctness.

**What to do:**
- Never accept a factual claim, API signature, library behavior, or citation without checking it against a real source — documentation, the actual codebase, or a test.
- Ask the model to cite where a claim comes from, or to show its reasoning ([Guide 1, Section 3.6](01-prompt-engineering.md#36-ask-for-reasoning-when-it-matters)) — this doesn't guarantee correctness, but it gives you something concrete to verify.
- If you catch a hallucination, don't just fix that one output — fix the prompt so it's less likely to recur (e.g., add "only reference functions that exist in the pasted code; do not invent APIs").

## "The agent changed files I never asked it to touch"

**What's happening:** The task was under-constrained — the agent inferred scope on its own because you didn't set explicit boundaries. See [Guide 2, Section 5.2](02-ai-agents-agentic-workflows.md#52-set-explicit-boundaries).

**What to do:**
- State out-of-scope files/directories explicitly in the prompt ("don't modify anything under `/migrations`").
- Ask for a plan before execution and actually read it ([Guide 2, Section 5.3](02-ai-agents-agentic-workflows.md#53-ask-for-a-plan-before-execution)) — this is the checkpoint designed to catch exactly this before it happens.
- If it already happened: review the diff/change history, revert anything outside scope, and tighten the prompt before retrying rather than just undoing the damage and moving on.

## "It seems to have forgotten something I told it earlier in the conversation"

**What's happening: context window overflow.** Every model has a maximum amount of text it can hold in memory at once (see [Glossary — context window](glossary.md#context-window)). In a long conversation, especially one with large pasted files, earlier content can get pushed out and the model genuinely no longer has access to it — it's not being careless, it literally cannot see it anymore.

**What to do:**
- For long or file-heavy tasks, start a fresh conversation for each distinct sub-task rather than one long running thread.
- Re-paste the specific context that matters right before asking a new question, rather than assuming it's still "in view."
- If using a custom GPT or Claude Code, remember that uploaded knowledge files and prior turns all count against the same limit — trim what's not needed for the current step.

## "I asked for one thing and got something else entirely"

**What's happening:** Usually a missing or ambiguous component in the prompt — most often a missing **Task** or **Format** specification (see [Guide 1, Section 2](01-prompt-engineering.md#2-the-five-components-of-a-strong-prompt)). The model filled the gap with its own guess, and the guess didn't match what you had in mind.

**What to do:**
- Re-read your prompt against the five-component checklist and identify what's actually missing.
- Don't just repeat the request — rewrite it to close the specific gap.

## "A custom GPT I built stopped following its instructions partway through a conversation"

**What's happening:** Long conversations dilute a system prompt's influence over time, especially once a lot of back-and-forth content has accumulated — this is related to the context-window issue above, not a bug specific to custom GPTs.

**What to do:**
- Start a new conversation with the assistant for a new task rather than continuing one long thread indefinitely.
- If a particular rule keeps getting dropped, restate it explicitly in your message rather than assuming the original instructions are still fully "in force."

## "Claude Code says it can't access a file or run a command"

**What's happening:** This is usually a permissions or working-directory issue, not a capability issue — e.g., you started the session outside the project folder, or the file is genuinely outside what you granted access to.

**What to do:**
- Confirm you started the session with `cd` into the correct project directory before running `claude` (see [Guide 4, Section 2](04-claude-code-basics.md#2-installing-it)).
- Ask it directly what it can see: `what files can you access from here?`
- Check the official troubleshooting docs linked in [references.md](references.md) for anything environment-specific (OS, permissions, install method).

## "I hit a usage limit or rate limit mid-task"

**What's happening:** Every plan — free or paid — has usage limits, and agentic tools like Claude Code can consume usage faster than chat because each Think→Act→Observe cycle is its own model call (see [Guide 2, Section 7](02-ai-agents-agentic-workflows.md#7-risks-and-guardrails-specific-to-agents) and [Guide 5, Section 3](05-choosing-the-right-tool.md#3-tool-options-and-current-accesspricing)).

**What to do:**
- Break large tasks into smaller, separately-verified steps rather than one long uninterrupted agent run — this also gives you more review checkpoints, which is good practice anyway.
- Check your plan's usage dashboard before starting a large task if you're close to a known deadline.

## "The output passed my read-through but failed the actual tests"

**What's happening:** This is exactly why [Guide 1, Section 6](01-prompt-engineering.md#6-evaluate-output-like-a-code-review) and [Guide 2, Section 5.4](02-ai-agents-agentic-workflows.md#54-verify-with-ground-truth-not-self-report) both insist on verifying against ground truth rather than a read-through or the AI's own summary. Code can look correct and still be wrong in ways that are only visible when actually executed.

**What to do:**
- Always run the real test suite yourself after any AI-assisted code change, rather than trusting a description of what changed.
- If tests fail, paste the actual failure output back to the tool rather than describing the failure from memory — exact error messages matter.

## "I'm not sure if I'm allowed to upload this file/data as 'knowledge' to a custom assistant"

**What's happening:** Not a technical failure, but a real risk — see [Guide 3, Section 6](03-custom-gpts-ai-assistants.md#6-guardrails-specific-to-custom-assistants).

**What to do:**
- Never upload student records, credentials, unpublished research data, or anything else sensitive to a shared or third-party-hosted assistant unless you've explicitly confirmed the platform's data handling and sharing settings.
- When in doubt, don't upload it — ask your institution's guidance on AI tool data handling first.

---
[← Previous: Choosing the Right AI Tool](05-choosing-the-right-tool.md) · [Back to course home](index.md) · [Next: Worked Case Study →](07-worked-case-study.md)
