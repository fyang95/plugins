### Prototype-first

**You own the pause. The sketch decides the shape, and the real build waits for a yes.**

Feature and any other playbook that would write production code run this gate first when the work is a new feature or a big front-end change. Small and reversible work skips it and stays autonomous under **Never Block on the Human**. The pause is a deliberate exception to that principle. The code would be reversible, and the gate still waits, because a wrong product shape costs more than a wrong line. **Experience First** is why the sketch comes first. The call flow, the user flow, and a big layout are the experience, and they are cheaper to redirect here than after the real build.

The Prototype playbook (`playbooks/prototype.md`) settles an empirical fork by observation. This gate asks the user to confirm a shape. Use the Prototype playbook from step 4 only when **Exhaust the Design Space** applies.

1. Classify before any production edit and before `architect` implements.

   **New feature.** Any one of these signals. A new backend API, endpoint, or RPC the system did not expose. A new workflow, meaning a new sequence of steps for a job the product did not do. A new user-facing capability, meaning a new job a person or a calling service can complete. A new field, flag, or option on a job that already exists is a change to existing behavior, unless it adds a new sequence of steps.

   **Big front-end change.** Any one of these signals. A new page, screen, route, or destination. A layout or navigation restructure, where what is on a page, where the regions sit, or how the user moves between areas changes. A multi-component redesign, where two or more components change their structure or how they compose, together. A new user-facing UI flow, a sequence of screens or states the user moves through that did not exist, including a multi-step modal, dialog, drawer, or panel.

   **Small.** No big signal fired, and the work is any of these. A color, spacing, typography, or copy tweak. A tweak inside one existing component that keeps the page structure, the navigation, and the sequence of steps. A bug fix that restores a screen to its existing behavior. A visual-parity migration whose bar is pixel-exact. A refactor that keeps the layout and the user path. A change to behavior that already exists, a perf change, or a new field or flag on an existing job. Mark the gate `skip: <reason>` and return to the matched playbook. Do not ask which class it is.

   **Both.** A new feature that is also a big front-end change runs this playbook once. Step 2, then step 4. The page sketches in step 4 are the front-end prototype.

2. For a new feature, lay out the two flows before any prototype. When the system already exists, read it with the **how** skill first so the call flow names the real boundaries. `how` is read-only. Skip it only for a greenfield with nothing to read. Reuse that report later in Feature so you do not ground twice.

   **Call flow.** How the pieces call each other, in order. Name the caller, the callee, and the request and response at each boundary. A sequence diagram or a numbered list is enough.

   **User flow.** How a user gets from the entry point to the outcome, including what they see or what a caller sends at each step. For a UI the user is the person at the screen. For an API or a library the user is the caller, per the **experience-first** principle skill.

   Show both flows. Ask whether they are right or what to change. Do not build the prototype and do not write production code until they answer. On a material change, revise the flows and show them again.

3. When the class is a big front-end change and not a new feature, mark step 2 `skip: no new feature` and continue at step 4. A new feature keeps step 2.

4. Build the cheapest prototype that makes the change clear. Put it in a scratch directory, separate from production source. No production framework, no tests, no persistence, no auth. Tell the user the prototype is throwaway.

   A feature with no UI uses the sequence diagram from step 2 when that diagram is already clear. Otherwise stub the endpoints, or write a one-file handler that returns fixture data.

   A UI feature, and any big front-end change, gets low-fi wireframes or one static HTML file per page. Show what each page looks like and how the front end is laid out. A clickable sketch is in bounds when it is still the cheapest way to show the path.

   When the interaction is novel and has no precedent, apply the **exhaust-the-design-space** principle skill. Build the recommended option and one or two alternatives behind one switcher, per the Prototype playbook, and include the choice in the question. A flow the user already specified gets that one flow.

   Show the prototype. Ask whether to implement it as-is or what to change. Stop. Do not start the matched playbook's implementation, do not run `architect`'s implement phase, and do not delegate production code. A requested change goes through this step again.

5. After the user confirms, return to the matched playbook and implement that confirmed flow. Feature is the build playbook for a new feature. Leave the scratch prototype out of the app.

**Autonomy.** "Don't stop", "going to bed", "be fully autonomous", and an autopilot or orchestrate grant do not answer this gate and do not skip the prototype. The grant covers the build after a yes. Produce the flows and the prototype, ask, and stop. Irreversible-action pauses in the Autonomy section still apply on top of this one.

**Reply:** the class and which signal fired, the flows when step 2 ran, the prototype path, and the question you are waiting on. While you are waiting, skip the implementation summary.
