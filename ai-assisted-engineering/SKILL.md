---
name: ai-assisted-engineering
description: Build reliable software with AI coding assistants and LLM application components. Use when Codex is asked to implement, plan, review, or optimize AI-assisted development workflows; build chat, RAG, agent, tool-calling, MCP, or streaming AI features; choose a Spring AI or LangChain4j-style integration approach; or reduce model/context cost without weakening tests, security, or verification.
---

# AI Assisted Engineering

## Overview

Apply practical AI-assisted development patterns while preserving ordinary software engineering discipline. Treat models as productive collaborators whose output must remain scoped, observable, testable, and safe to operate.

## Workflow

1. Establish the deliverable before generating or changing code.
   - Identify the user-visible outcome, existing stack, touched boundaries, external effects, secrets, and acceptance checks.
   - Inspect the repository patterns and relevant official documentation when libraries, model capabilities, or pricing may have changed.

2. Control context deliberately.
   - Read the smallest set of relevant source files, configuration, tests, and docs needed for the task.
   - Exclude dependencies, build artifacts, logs, large unrelated directories, and sensitive local configuration from model context.
   - Split unrelated phases into focused tasks or summarize validated decisions before moving on.

3. Choose an implementation path proportional to risk.
   - For small, well-specified changes, implement directly and run focused verification.
   - For new architecture, external actions, broad changes, or ambiguous requirements, form a short plan and validate assumptions before expanding the implementation.
   - Prefer framework and project conventions already present over novelty.

4. Build AI functionality in incremental capabilities.
   - Start with a narrow model call and a testable service boundary.
   - Add only needed capabilities: prompt configuration, session memory, structured output, retrieval, tools/MCP, streaming, observability, and safety controls.
   - For chat, RAG, agent, tool-calling, MCP, or streaming features, read [references/ai-application-checklist.md](references/ai-application-checklist.md).

5. Verify outcomes, not just generation.
   - Run the existing narrowest meaningful tests, type checks, linters, builds, or smoke tests.
   - Exercise model-dependent paths with controlled inputs or mocks where practical; state clearly when live-provider testing cannot be run.
   - Inspect security, privacy, cost, failure modes, and observability before treating an AI path as production-ready.

## Cost And Model Discipline

- Use a cheaper or faster model for routine transformations only when the product or tool exposes a choice and expected quality is measurable.
- Use stronger reasoning where architectural judgment, difficult debugging, security review, or high-impact changes need it.
- Minimize irrelevant input context and unnecessary prose output; preserve the evidence needed to reason correctly and verify.
- Track usage or set budgets for model-backed applications when supported.
- Verify current model names, pricing, quotas, and provider capabilities from primary documentation before making a time-sensitive recommendation.

## Non-Negotiable Guardrails

- Do not omit necessary tests, review, documentation, error handling, or security work merely to reduce tokens.
- Do not use insults, fabricated consequences, jailbreak folklore, or other manipulative prompt tricks as an engineering method.
- Do not place API keys or sensitive configuration in tracked files or model-visible context unless explicitly required and safely handled.
- Do not give autonomous tools unbounded side effects; require appropriate approvals, validation, and logging for destructive, financial, account, or production actions.
- Do not treat tutorial claims, model output, benchmark claims, or vendor marketing as proof; confirm critical behavior with code, tests, and primary sources.

## Expected Output

When applying this skill, produce a scoped implementation or recommendation, the verification performed, and any remaining provider/runtime assumptions. Keep cost optimization subordinate to correctness and maintainability.
