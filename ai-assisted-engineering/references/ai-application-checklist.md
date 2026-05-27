# AI Application Checklist

Read this reference when implementing or reviewing an application that embeds model calls, chat, retrieval, agents, tools, MCP, or streamed responses.

## Capability Progression

Add capabilities only when required by the product behavior:

1. Model client behind a service boundary with provider configuration externalized.
2. Prompt or instruction configuration kept maintainable and reviewable.
3. Conversation memory keyed by user or session with retention and privacy decisions.
4. Structured output parsed and validated rather than trusted as free text.
5. Retrieval with source selection, chunking/embedding strategy, and citation behavior.
6. Tool calling or MCP with narrowly scoped tools, schema validation, timeouts, and approval boundaries.
7. Streaming output such as SSE where latency materially affects interaction quality.
8. Observability, evaluation, guardrails, rate limits, and cost reporting.

## Integration Questions

- What exact task should the model perform, and what must conventional code validate?
- Which provider/model capability is required: text, multimodal input, structured output, tools, embeddings, or streaming?
- Where do credentials live, and are local secret files ignored by version control?
- What data may leave the system, and is any of it sensitive or regulated?
- How does failure appear to users: timeout, partial stream, malformed output, unavailable retriever, or tool error?
- How will behavior be regression-tested when model outputs vary?

## Chat And Streaming

- Give chat calls a stable service boundary rather than wiring providers throughout controllers or UI code.
- Scope memory per session/user; define expiry, maximum history, and privacy handling.
- Stream responses only when useful, and handle disconnects, errors, incomplete responses, and cancellation.
- Keep frontend/backend contracts explicit for message ids, session ids, events, and error events.

## Retrieval

- Test retrieval separately from generation using known queries and expected sources.
- Treat retrieved content as untrusted input; protect system instructions and tool permissions from prompt injection.
- Expose citations or source identifiers when factual grounding matters.
- Measure whether retrieval improves relevant answers before making it mandatory.

## Tools And MCP

- Keep tools narrow and typed; validate arguments and returned data.
- Require confirmation for destructive operations or meaningful external side effects.
- Restrict network, file, identity, payment, production, and secret access to the minimum necessary.
- Log tool invocation metadata safely without leaking secrets or personal data.

## Verification

- Unit test deterministic assembly, parsing, authorization, retrieval selection, and tool handlers.
- Add integration or contract tests for provider adapters and streaming protocols where feasible.
- Use fixed evaluation prompts/examples for important user workflows and inspect regressions.
- Review token usage, latency, errors, and tool-call outcomes in deployed paths.

## Distilled Source And Limits

These practices were initially distilled from useful portions of `liyupi/ai-guide`, particularly its project tutorial covering LangChain4j chat, memory, retrieval, tools/MCP, streaming, and observability, together with its useful advice on focused context and cost awareness.

The source also contains promotional or informal advice. Exclude suggestions that trade away tests or rely on manipulative prompts, and confirm changing framework/provider details using official documentation.
