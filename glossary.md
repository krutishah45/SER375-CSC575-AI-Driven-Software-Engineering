---
title: Glossary
nav_order: 9
---

[← Back to course home](index.md)

# Glossary

Plain-language definitions for terms used across all four guides. Terms are alphabetical — use Ctrl+F / Cmd+F to jump to what you need.

**Agent**
A system where an AI model decides its own next action based on what it observes, in a loop, rather than following a fixed sequence you wrote in advance. See [Guide 2](02-ai-agents-agentic-workflows.md).

**Agentic workflow**
A broader term covering both fixed *workflows* and dynamic *agents* — any system where an AI model's output triggers further automated steps. See [Guide 2](02-ai-agents-agentic-workflows.md).

**API (Application Programming Interface)**
A way for software to talk to another piece of software directly, without a human clicking through a chat interface. When a course guide mentions "the API," it means using the AI model programmatically instead of through a chat window — usually billed per token rather than a flat monthly fee.

**Chain-of-thought prompting**
Asking a model to show its reasoning step by step before giving a final answer. Often improves accuracy on tasks with multiple steps or trade-offs. See [Guide 1, Section 3.6](01-prompt-engineering.md#36-ask-for-reasoning-when-it-matters).

**Context**
The information available to the model when it generates a response — your current prompt, plus anything earlier in the conversation, plus (for agentic tools) any files it has read. Distinguish from *context window* below.

**Context window**
The maximum amount of text (measured in tokens) a model can "see" at once — your prompt, any files, and its own prior responses all count against this limit. If a conversation or document is too long, older content gets pushed out and the model can no longer refer back to it.

**Custom GPT**
OpenAI's term for a saved, reusable AI assistant configuration: instructions + optional knowledge files + optional tools, packaged so it doesn't need to be re-explained every time. See [Guide 3](03-custom-gpts-ai-assistants.md).

**Few-shot prompting**
Giving the model 1 or more examples of the output style you want before asking it to produce a new one. Contrast with *zero-shot prompting*. See [Guide 1, Section 3.4](01-prompt-engineering.md#34-use-examples-few-shot-prompting).

**Fine-tuning**
Further training a model on a specific dataset so its default behavior changes permanently for that copy of the model. This is different from prompting or a custom GPT — fine-tuning changes the model itself, while prompting and custom GPTs only change what you send *to* an unchanged model. Not covered hands-on in this course, but the distinction matters if you read about it elsewhere.

**Hallucination**
When a model states something false, fabricated, or unsupported as if it were fact — confidently and often plausibly. Models don't "know" when they're wrong, which is why verification against ground truth (tests, documentation, a second source) is always your responsibility. See [Guide 1, Section 6](01-prompt-engineering.md#6-evaluate-output-like-a-code-review).

**Knowledge (in a custom GPT)**
Files you upload to a custom GPT so it can reference their content when answering — distinct from *instructions*, which govern behavior rather than facts. See [Guide 3, Section 2](03-custom-gpts-ai-assistants.md#2-what-a-custom-gpt-is-made-of).

**Large Language Model (LLM)**
The type of AI model behind tools like ChatGPT and Claude — trained on large amounts of text to predict likely next words, which in practice lets it answer questions, write, and reason across many domains.

**Prompt**
The text you send to an AI model. See [Guide 1, Section 1](01-prompt-engineering.md#1-what-is-a-prompt-really).

**Prompt chaining**
An agentic pattern where the output of one AI call becomes the input to the next, in a fixed sequence. See [Guide 2, Section 6](02-ai-agents-agentic-workflows.md#6-common-agent-workflow-patterns).

**Prompt engineering**
The practice of designing a prompt's wording, structure, and context so the model's output reliably matches your intent. See [Guide 1](01-prompt-engineering.md).

**Prompt injection**
An attack where hidden or disguised instructions inside content the model reads (a web page, an uploaded file, a code comment) attempt to override your actual instructions. A key reason to treat any external content fed to an AI tool as untrusted input. See [Guide 1, Section 7](01-prompt-engineering.md#7-common-pitfalls).

**Prompt log**
A running record of the prompts you used, the tool, a summary of the output, and what you did with it (accepted, revised, rejected). Required for several exercises in this course and useful practice generally — it makes AI-assisted work reproducible and defensible.

**RAG (Retrieval-Augmented Generation)**
A technique where a system looks up relevant information from an external source (documents, a database) and inserts it into the model's context before generating a response, rather than relying only on what the model learned during training. This is how "knowledge" files in a custom GPT function under the hood.

**Role prompting / persona**
Telling the model what expertise or perspective to adopt in its response (e.g., "act as a senior QA engineer"). See [Guide 1, Section 2](01-prompt-engineering.md#2-the-five-components-of-a-strong-prompt).

**System prompt**
Instructions set once, "behind the scenes," that shape a model's behavior for an entire session or assistant, rather than being retyped in every message. A custom GPT's *instructions* function as a system prompt.

**Temperature**
A setting (usually 0–1 or 0–2 depending on the platform) controlling how random or deterministic a model's output is. Lower temperature gives more consistent, predictable output; higher temperature gives more varied, creative output. Not something you'll configure directly in a chat interface, but relevant if you use the API.

**Token**
The unit AI models process text in — roughly ¾ of a word in English on average, though it varies. Pricing, context window limits, and usage caps are usually measured in tokens, not words or characters.

**Tool use / function calling**
A model's ability to call an external tool (search the web, run code, query an API) as part of generating its response, rather than answering purely from what it already "knows." This is the mechanism that makes agents possible.

**Workflow**
A system where an LLM and tools are orchestrated through a fixed, predefined sequence of steps written in code — contrast with *agent*, where the model decides the sequence itself. See [Guide 2, Section 2](02-ai-agents-agentic-workflows.md#2-workflows-vs-agents--an-important-distinction).

**Zero-shot prompting**
Asking a model to perform a task with no examples provided — just an instruction. Works for simple, well-defined tasks; struggles with anything stylistically specific. Contrast with *few-shot prompting*.

---
[← Back to course home](index.md)
