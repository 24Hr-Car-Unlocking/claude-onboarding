# Use case 4 — Understanding issues, problems & solutions

Before you write any spec, use Claude as a **codebase cartographer** and **rubber duck**. Read-only, no edits, just understanding.

----

## The "explain it to me" pattern

Always launch in **plan mode** for this work. No edits possible.

```
Read phoenix-docs/documentation/agents/phoenix.md and the 
phoenix repo. In your own words, explain how the customer 
unlock flow works end-to-end. Trace every file involved 
in order. Do not edit anything.
```

Claude returns a written walkthrough. You ask follow-ups. By the end, you understand the system well enough to write a spec for it.

----

## The "trace this" pattern

When you have a specific user action in mind:

```
Trace what happens when a customer taps "Unlock" in the 
customer-app. Start from the button handler and follow the 
code through to the database. List every file touched in 
order, with a one-line summary of what each does.
```

Output: a numbered list of file paths with explanations. Save it as a markdown note for future reference.

----

## The "what are my options" pattern

When you have a problem but no obvious solution:

```
Problem: We need to send unlock confirmations to technicians 
in real time. Currently we poll every 30 seconds which is 
expensive and laggy.

Read the relevant repos and propose 3 solutions. For each:
- How it works (high level)
- Pros / cons
- Effort estimate (S/M/L)
- What repos it touches

Do not implement anything.
```

This is your input for an **ADR** if the decision is permanent.

----

## ADRs — Architecture Decision Records

When you make a permanent technical decision (database choice, framework, auth flow, hosting platform), capture it in an ADR.

```bash
cd D:/repos/phoenix-workspace/phoenix-docs
cp templates/adr-template.md specs/adrs/ADR-007-realtime-transport.md
```

The template forces:

- **Context** — what situation prompted this?
- **Decision** — what did we pick? (specific, named tech)
- **Alternatives** — what else did we consider, with pros/cons
- **Consequences** — benefits, tradeoffs, migration plan
- **Repos affected**

ADRs are **permanent** — never archived, never deleted, only superseded.

Note:
3 months from now you'll forget why you picked WebSockets over Server-Sent Events. The ADR is your future self's lifeline. Even a 1-page ADR beats the best memory.

----

## The rubber-duck pattern

When you're stuck and don't even know what question to ask:

```
I'm trying to figure out [vague problem statement]. I don't 
know what I don't know. Ask me 10 questions that would help 
clarify the problem before either of us tries to solve it.
```

Claude is excellent at this. The questions surface assumptions you didn't realize you were making.

Note:
This pattern is genuinely how senior engineers think. The first 30 minutes of any hard problem is figuring out what the actual problem is. LLMs are great at the question-asking phase.
