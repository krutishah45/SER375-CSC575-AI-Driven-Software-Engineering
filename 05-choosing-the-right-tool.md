---
title: "Guide 5: Choosing the Right AI Tool"
nav_order: 6
---

[← Back to course home](index.md)

# Guide 5: Choosing the Right AI Tool

**Prerequisite:** Guides 1–4. This page doesn't teach new concepts — it helps you decide, in the moment, which of the tools you've already learned about is the right one for the task in front of you.

## 1. Start here: the decision tree

![Decision tree for choosing an AI tool: starts with "what's the task," branches into a one-off question (plain chat), a repeatable task (custom GPT), or a task needing real file/codebase access, which further branches into a fixed-steps workflow versus an open-ended agentic coding tool like Claude Code](assets/tool-decision-tree.svg)

| If your task is... | Reach for... | Why |
|---|---|---|
| A one-off question, explanation, or quick draft | Plain chat (ChatGPT, Claude, etc.) | No setup cost is justified for something you'll only do once |
| Something you'll do the same way repeatedly, possibly with a team | A custom GPT / assistant | Instructions and reference material get saved once and reused — see [Guide 3](03-custom-gpts-ai-assistants.md) |
| Reading, editing, or testing real code in a real project, with the exact steps known in advance | A scripted automation / fixed workflow | More predictable and cheaper than a full agent when the path doesn't need to be dynamic — see [Guide 2, Section 2](02-ai-agents-agentic-workflows.md#2-workflows-vs-agents--an-important-distinction) |
| Reading, editing, or testing real code where the right steps depend on what's discovered along the way | An agentic coding tool (e.g., Claude Code) | This is exactly the open-ended, verifiable-by-tests situation agents are suited for — see [Guide 4](04-claude-code-basics.md) |

## 2. Mapping tools to SDLC phases

The table below lists what each category of tool is generally used for at different SDLC phases, based on how each is documented and commonly used. Treat this as **a starting menu of options, not a ranking** — no single tool is authoritatively "best" for a phase; the right choice depends on your specific task, and the guides above (Sections 1–4) give you the criteria to decide for yourself.

| SDLC Phase | Tools commonly used | Notes |
|---|---|---|
| Requirements / Vision Document | Plain chat, custom assistant | Mostly single-turn or template-fill tasks — full agent capability isn't usually needed here |
| Design / Architecture | Plain chat, custom assistant (with chain-of-thought prompting) | Benefits from asking the model to reason through trade-offs (Guide 1, Section 3.6) before committing to a design |
| Implementation (writing code) | Agentic coding tool (e.g., Claude Code), or plain chat for small snippets | Larger or multi-file changes benefit from an agent that can read the existing codebase directly |
| Code review | Custom assistant with a fixed checklist, or plain chat | The Critique-Against-Criteria pattern from Guide 1, Section 3 works well as a saved custom GPT |
| Testing | Agentic coding tool | Test generation and running the suite both benefit from direct file/command access |
| Debugging | Agentic coding tool | The Think→Act→Observe loop (Guide 2, Section 3) matches how debugging actually works |
| Documentation | Plain chat or custom assistant | Audience-Targeted pattern from Guide 1; rarely needs agentic file access |

## 3. Tool options and current access/pricing

The table below lists the tools referenced across this course, what's free vs. paid, and any important caveats. **Pricing and feature availability change frequently — this table reflects what was verified against each vendor's own pricing/help pages as of August 2026. Always check the live page (linked) before making a decision for your project or team.**

| Tool | Free tier? | What unlocks with a paid plan | Caveat to know |
|---|---|---|---|
| **ChatGPT** (OpenAI) | Yes — limited usage, ads on some tiers | Plus ($20/mo) and above add higher usage limits, more capable models, and access to *use and edit* custom GPTs | As of the official OpenAI Help Center documentation, **creating new custom GPTs is not available on personal accounts at any paid tier** (Free, Go, Plus, or Pro) — it requires a Business, Enterprise, or Edu workspace account. Personal accounts can still use existing GPTs. Confirm current status at the link below before planning an assignment around building one. |
| **Claude** (Anthropic) | Yes — chat, code generation, web search, memory, file creation | Pro ($17–20/mo) and above add **Claude Code**, Claude Cowork, higher usage limits, and access to more models | Claude Code is **not available on the Free plan at all** — it requires Pro or a higher paid tier (or pay-as-you-go API credits) |
| **Claude Code** (Anthropic) | No | Included in Claude Pro, Max, Team, and Enterprise plans; also usable pay-per-token via API without a subscription | Shares the same usage pool/limits as your regular Claude chat usage on subscription plans |

## 4. Practical guidance for this course

- For exercises that only require a saved, reusable assistant configuration (Guide 3), a personal ChatGPT or Claude account may be enough — check current custom-GPT creation availability (Section 3 above) before assuming your account tier supports it.
- For Guide 4 exercises using Claude Code, you'll need at least a paid Claude plan or API access — there is no free path to Claude Code specifically.
- When in doubt about what a specific account tier includes, verify on the vendor's own pricing page rather than a blog post or forum — pricing pages change faster than third-party write-ups can track.

## Further Reading

- Anthropic — [Claude pricing & plans](https://claude.com/pricing) (official, includes free/paid feature comparison and Claude Code availability)
- OpenAI — [Creating and editing GPTs](https://help.openai.com/en/articles/8554397-creating-and-editing-gpts) (official Help Center — current custom GPT creation eligibility)
- OpenAI — [ChatGPT pricing](https://chatgpt.com/pricing/) (official — check before assuming what a given tier includes)

---
[← Back to course home](index.md) · [Next: FAQ / Troubleshooting →](06-faq-troubleshooting.md)
