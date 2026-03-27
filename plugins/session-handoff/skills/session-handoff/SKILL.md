---
name: session-handoff
description: Creates comprehensive handoff documents for seamless AI agent session transfers. Triggered when: (1) user requests handoff/memory/context save, (2) context window approaches capacity, (3) major task milestone completed, (4) work session ending, (5) user says 'save state', 'create handoff', 'I need to pause', 'context is getting full', (6) resuming work with 'load handoff', 'resume from', 'continue where we left off'. Proactively suggests handoffs after substantial work (multiple file edits, complex debugging, architecture decisions). Solves long-running agent context exhaustion by enabling fresh agents to continue with zero ambiguity.
---

# Session Handoff Skill

Generates a structured, deterministic session summary designed to be fed into a new Claude Code session or used with `/compact` to preserve continuity without relying on auto-compact's generative summarization.

## The Problem This Solves

Auto-compact summarizes freely — it infers, fills gaps, and occasionally fabricates continuity. The result is non-deterministic and degrades session fidelity, especially for complex consulting and architecture work where rationale, constraints, and rejected options are as important as decisions made.

This skill produces a terse, fact-only summary that can be fed verbatim into a new session as a deterministic context handoff.

---

## When to Trigger

Trigger this skill when:
* User mentions context limit, compacting, or starting a new session
* `Ctx` percentage is approaching 60% (the recommended threshold for consulting work)
* User says "save where we are", "session summary", "handoff", or similar
* A long architecture or consulting session is wrapping up a phase

---

## The Summary Prompt

Use this prompt verbatim when generating the handoff. Do not deviate from the structure or add sections not listed here.

Summarize this session using exactly these sections:

1. Decisions made (include rationale for each decision)
2. Active constraints (client-specific, technical, scope)
3. Committed AWS service choices (services already selected and why)
4. Rejected options (include the reason each was rejected)
5. Current state of work (what is done, in-progress, not started)
6. Open questions (unresolved items that must carry forward)
7. Key entities (client name, system names, integrations, stakeholders)

Rules:
- Be terse. One to two sentences per item maximum.
- No inferred information. If it was not explicitly stated in this session, omit it.
- No filler, transitions, or commentary between sections.
- Omit any section that has nothing explicitly stated.
- Do not summarize the summary. Output the sections only.

---

## Output Format

Wrap the output in a clearly labeled block the user can paste directly into a new session or feed to `/compact`:

Session Handoff — [date] [brief topic label]

[summary sections here]

---Generated at Ctx: XX% — feed this block verbatim into the next session.

---

## Key Principles

* **"No inferred information" is the critical instruction.** Claude will pad and infer by default. This line suppresses that behavior and is what makes the output deterministic.
* **Act before 60% Ctx.** Summary quality degrades under context pressure. A faithful summary requires enough working window to generate it accurately.
* **Rationale is the highest-value content.** Decisions without rationale force re-litigating closed issues in the next session. Capture the why, not just the what.
* **Rejected options are equally important.** They prevent the next session from retreading ground already covered.
