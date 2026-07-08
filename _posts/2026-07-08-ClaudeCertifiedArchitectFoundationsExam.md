---
layout: post
title: "How I Cleared the Claude Certified Architect Foundations Exam"
---
![_config.yml]({{ site.baseurl }}/images/claude/im1.png)

I recently cleared the **Claude Certified Architect Foundations** certification with a score of **776**, above the passing score of **720**.

This was not a prompt-engineering trivia exam. It felt much closer to an architecture judgement exam for people building AI-native systems with Claude.

That is what made it valuable for me.

I have been vibe coding and architecting enterprise productivity solutions using Claude Code, MCPs, RAG, Elastic Agent Builder, Agentforce, and the Claude platform. I wanted to challenge whether my understanding of AI-native solution design was strong enough beyond demos and experiments.

Enterprise AI is clearly moving in this direction. The future will not be won by teams that only know how to prompt. It will be won by teams that know how to design reliable, observable, deterministic, and safe AI systems.

## Why I Took the Exam

![_config.yml]({{ site.baseurl }}/images/claude/im2.jpg)

My motivation was practical.

I have been solving productivity gaps in enterprise workflows using AI-native patterns. That means building systems where agents can reason, use tools, retrieve context, follow constraints, and escalate when needed.

But hands-on work can create blind spots. You can build something that works in your environment and still miss important architectural principles.

The certification gave me a structured way to test that.

I wanted to see whether my intuition around Claude Code, MCP, RAG, agentic systems, structured output, and enterprise reliability was aligned with how Anthropic frames production-grade Claude architecture.

## What the Exam Covers
![_config.yml]({{ site.baseurl }}/images/claude/im3.png)

The certification focuses on practical Claude architecture across five major areas:

- **Agentic Architecture & Orchestration**
- **Tool Design & MCP Integration**
- **Claude Code Configuration & Workflows**
- **Prompt Engineering & Structured Output**
- **Context Management & Reliability**

The exam is scenario-based, which matters. It does not simply ask whether you know a term. It asks whether you can choose the right architectural response for a realistic production problem.

That distinction is important.

In real enterprise systems, the right answer is rarely “write a better prompt”. Sometimes the answer is schema enforcement. Sometimes it is a hook. Sometimes it is a scoped tool. Sometimes it is human escalation. Sometimes it is not using an agent at all.

## My Preparation Timeline
![_config.yml]({{ site.baseurl }}/images/claude/im4.jpg)

I spent around **three weeks** preparing.

Most of that time went into completing the lessons in **Anthropic Academy** and going through the pre-course work. I also used this community guide as a secondary reference:

[Claude Certified Architect community guide](https://github.com/paullarionov/claude-certified-architect/blob/main/guide_en.md)

The official material gave me the structure. The community guide helped me review concepts in a consolidated way. But the biggest advantage came from already having practical exposure to Claude Code, MCPs, RAG, and agentic platforms.

This exam rewards applied judgement. Reading helps, but hands-on experience makes concepts stick.

## My Starting Point
![_config.yml]({{ site.baseurl }}/images/claude/im5.png)

I was not starting from zero.

Before taking the exam, I had already been working on enterprise productivity use cases using:

- Claude Code
- MCPs
- RAG-based architectures
- Elastic Agent Builder
- Salesforce Agentforce
- Claude platform concepts
- Agentic workflows for enterprise automation

That experience helped me reason through scenario-based questions. The exam often asks you to pick the best architectural choice, not just identify a definition.

## The Most Important Lesson
![_config.yml]({{ site.baseurl }}/images/claude/im6.png)

The biggest lesson from this exam is simple:

**Determinism in AI systems does not come from prompting alone.**

A prompt can guide behaviour, but it cannot guarantee compliance in critical workflows. When business rules matter, the system needs stronger controls.

That is where architecture comes in.

Hooks, tool permissions, JSON schemas, scoped MCP tools, structured errors, validation loops, and escalation paths are what make AI systems production-ready.

The exam reinforces that distinction repeatedly. It expects you to know when model discretion is acceptable and when enforcement must move into the system design.

## Topics I Would Study Deeply
![_config.yml]({{ site.baseurl }}/images/claude/im7.png)

If you are preparing, I would focus on these areas.

## 1. Agentic Loops and Orchestration

Understand how an agentic loop works.

The model responds. The system inspects whether the response requires tool use or whether the turn is complete. Tool results are added back into context so the model can reason through the next step.

This sounds simple, but it is foundational. If you do not understand the loop, it becomes harder to reason about orchestration, handoffs, escalation, and reliability.

## 2. MCP Tool Design

MCP is not just about exposing tools. It is about exposing the right tools with the right boundaries.

Good tool design includes:

- Clear descriptions
- Input format expectations
- Output contracts
- Error categories
- Retryability
- Boundary guidance
- Examples of when to use one tool versus another

Weak tool descriptions create unreliable tool selection. If two tools sound similar, the model can easily choose the wrong one.

That is not a model failure. That is an interface design failure.

## 3. Hooks and Enforcement

This was one of the clearest architectural lessons.

If something must always happen, do not rely only on prompt instructions.

Use programmatic enforcement.

For example, if a workflow requires a prerequisite step before a sensitive action, the system should enforce that through hooks, permissions, or gates.

This maps directly to enterprise architecture. Any workflow involving money, customer records, security, compliance, or production changes needs deterministic safeguards.

## 4. Structured Output and Extraction

Scenario-based questions around extraction and error handling were among the most complex.

This area is important because many enterprise AI use cases involve turning messy documents into structured records.

The key ideas are:

- Use JSON schema where strict structure is required
- Make fields optional or nullable when source data may be missing
- Include enum values for uncertainty
- Add validation loops
- Use few-shot examples for ambiguous document patterns
- Avoid forcing the model to fabricate values just to satisfy a schema

Structured extraction is where prompt quality, schema design, validation, and error handling meet.

## 5. Claude Code Configuration

Claude Code configuration requires more precision than people expect.

You need to understand when to use:

- `CLAUDE.md`
- `.claude/rules/`
- Skills
- Slash commands
- Hooks
- Settings permissions
- Plan mode
- Direct execution

These are not interchangeable.

Some instructions are always-loaded project context. Some are path-specific. Some should be invoked on demand. Some belong in hooks because they require enforcement. Some belong in settings because they are permission boundaries.

This is one area where my score report showed clear gaps, which made the feedback useful. I passed, but I also learned where I need to sharpen my Claude Code configuration judgement.

## 6. Context Management and Reliability

Context is not infinite just because context windows are larger.

Long workflows can degrade. Tool outputs can flood the conversation. Important facts can get buried. Subagents may not inherit context unless it is explicitly passed. Summaries can lose critical numbers, dates, IDs, or source attribution.

For production systems, context management needs design.

Use structured case facts. Preserve source mappings. Keep scratchpad files. Isolate verbose exploration in subagents. Pass only relevant context downstream. Do not assume the model will remember what the system did not preserve.

This is where enterprise AI work becomes less like prompting and more like systems engineering.

## What Surprised Me
![_config.yml]({{ site.baseurl }}/images/claude/im8.png)

The scenario-based questions around extraction and error handling were more nuanced than I expected.

That was also the most valuable part.

In production, error handling is not just “try again”. The system needs to know whether an error is transient, validation-related, permission-related, or a business-rule violation.

A timeout may be retryable. A policy block may not be. A valid empty result is not the same as a failed search. A missing field should not cause hallucination. A human escalation should preserve context, authorisation state, and findings.

These details are what make agentic systems reliable.

## What My Score Report Taught Me

My score report was useful because it showed both strengths and gaps.

I scored strongly in areas such as orchestration safeguards, structured handoffs, PreToolUse and PostToolUse hooks, agentic loop stop reasons, slash commands, MCP project scope, structured output, extraction schemas, Message Batches versus synchronous APIs, and MCP error handling.

I also had weaker areas, including dynamic task decomposition, Claude Code configuration mechanism selection, enforcement versus `CLAUDE.md` placement, context management in large codebase exploration, and escalation decision criteria.

That made the certification more credible for me.

Passing does not mean mastery. It means you have enough foundation to keep building, while knowing where your gaps are.

## My Final 48-Hour Strategy

In the final 48 hours, I would not recommend passive reading.

Ask Claude to challenge you.

Use the official study guide domains and ask Claude to generate scenario-based questions. Then explain your answer before checking. Ask why the other options are wrong. Ask it to make the next question harder.

Focus especially on:

- Extraction
- Error handling
- Tool choice
- Hooks
- Escalation
- Claude Code configuration
- Context management
- MCP tool design

Do not just memorise terms. Practise architectural reasoning.

## My Advice for Anyone Preparing
![_config.yml]({{ site.baseurl }}/images/claude/im9.jpg)

Treat the exam like an architecture review.

When you read a scenario, ask:

- What is the actual failure mode?
- Is this a prompt problem or an enforcement problem?
- Does this need a schema, hook, permission, or human review?
- Is the tool too generic?
- Is the context too noisy?
- Is the workflow blocking or asynchronous?
- Should the model decide, or should the system constrain?

That mindset is far more useful than memorising definitions.

## Conclusion
![_config.yml]({{ site.baseurl }}/images/claude/im10.png)

Clearing the Claude Certified Architect Foundations exam was a good milestone, but the larger takeaway was about how enterprise AI is evolving.

We are moving from AI demos to AI-native systems. That shift requires more than clever prompts. It requires architecture.

The systems that matter will need reliable tool use, scoped permissions, structured outputs, explicit context management, strong error handling, human escalation, observability, and deterministic controls where business risk demands them.

For me, this certification was a useful checkpoint. It validated parts of what I have been building with Claude Code, MCPs, RAG, Elastic Agent Builder, Agentforce, and Claude platform patterns. It also gave me a sharper map of where to keep improving.

AI-native architecture is becoming a core enterprise skill. The sooner we treat it as engineering rather than experimentation, the better the systems we will build.

## AI Assistance Note

I used AI assistance to organise my reflections, structure this post, and convert my rough preparation notes into a readable article. The experience, score, preparation approach, and opinions are my own.

Keywords: #Claude #Anthropic #ClaudeCode #MCP #AIAgents #AgenticAI #EnterpriseAI #AIArchitecture #RAG #StructuredOutput #PromptEngineering #ClaudeCertifiedArchitect #Elastic #Agentforce
