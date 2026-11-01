---
name: principle-never-block-on-the-human
description: "Apply when tempted to ask 'should I do X?' on reversible work. A new feature or a big front-end change is the Prototype-first exception and waits."
disable-model-invocation: true
---

# Never Block on the Human

The human supervises asynchronously. Agents must stay unblocked. Make reasonable decisions, proceed, and let the human course-correct after the fact. Since code changes are reversible and reviewable, a wrong decision usually costs less than blocking.

- Proceed, then present. Do the work, show the result. Don't ask "should I do X?" Do X, explain why.
- Make the system self-healing. When you notice a problem, log it and fix it in the next round.
- Irreversible actions (force-push, delete production data, send external messages) still require confirmation.
- Reversible actions (write code, edit notes, split tasks) should proceed without blocking.
- Product direction comes from the human. Execution should not block.

**Exception.** A new feature or a big front-end change pauses on purpose. Poteto mode runs the Prototype-first playbook (`../poteto-mode/playbooks/prototype-first.md`) and waits until the user confirms the flows and the prototype, before any production code. The code would be reversible. The pause still holds, because the product shape is the expensive part. A color, spacing, copy, or single-component tweak, and any other small reversible change, still proceeds without asking. A grant to keep going does not answer the pause.
