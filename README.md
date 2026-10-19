# AI Maintenance Coordinator

A one-page demo of an AI maintenance coordinator for property management firms. You play a tenant texting the firm; a live Claude agent triages the request, walks the tenant through self-fixes, picks a vendor from the firm's own bench, proposes times, and asks the owner for approval when a job exceeds the dollar limit.

**Live demo:** https://claude.ai/artifact/Y7ZqrfAdyByZUA3EQZb2jB (private to the owner until shared)

## What's on the screen

1. **Tenant's phone** — an SMS-style thread. Pick a scenario, send the opening text or write your own, and use the quick replies or free text to push back.
2. **Agent decisions** — the triage lane (emergency, tenant can fix, needs vendor, not maintenance), the agent's reasoning, self-fix steps, the vendor it picked from the bench and why, proposed times, and the estimate against the approval limit.
3. **Owner & manager** — approval requests with Approve/Decline (the agent picks the conversation back up after you decide), the manager inbox for non-maintenance escalations, the work order, and an activity log.

## Scenarios

| Scenario | Expected handling |
| --- | --- |
| Active leak | Emergency: shutoff instructions, 24/7 plumber dispatched under the emergency exception |
| Garbage disposal | Tenant self-fix: reset button / hex key, no visit |
| No heat in winter | Habitability emergency: heating vendor dispatched now |
| AC out | Normal priority: HVAC vendor, owner approval if over the limit |
| Noise complaint | Not maintenance: routed to the property manager |
| Free play | Anything you want to try |

## How it works

`index.html` is a single self-contained page published as a claude.ai Artifact. It calls Claude through the Artifact runtime's `sample` capability (`claude.use("sample")` → `sample.json(...)`), so there is no backend and no API key: each message runs on the viewer's own Claude account, and the viewer is asked once to allow it. Each turn sends the firm policy, vendor bench, scenario context, current work order and transcript, and gets back a JSON decision that drives all three panes. The page also enforces the approval limit itself, so an over-limit, non-emergency estimate always produces an approval request.

Opened as a plain file outside Claude, the page renders with one recorded example turn, but the live agent is disabled.

The firm, tenants, owners, vendors and prices are fictional. Nothing is actually texted; vendor confirmations are simulated.
