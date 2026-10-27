# Hermes: a self-hosted, always-on product-management agent

> An LLM agent that lived on a VPS and never slept. It ran product management
> for an app, turning conversations and signals into tickets and keeping the
> backlog honest, and doubled as a 24/7 assistant.

Hermes is the agent I built as **CEO** of a small software company to keep
product moving without being the bottleneck. Unlike a local, on-demand agent
you summon from your laptop, Hermes was a **persistent service**: up around the
clock, reachable from anywhere, and reacting to events on its own.

This repository is a **sanitized, generalized showcase** of that system: the
architecture and the operating model, with the specific app, company and tools
removed. It's meant to be read, not run as-is.

> **Part of a system.** [`larry`](https://github.com/soeren90/larry) shows the
> *other* deployment model: an on-demand orchestrator running a fleet of
> specialist sub-agents locally. Hermes is the always-on, single-service
> counterpart. Both are **bodies that read from a shared brain**,
> [`shared-brain`](https://github.com/soeren90/shared-brain), the plain-Markdown
> store of memory, skills and agent definitions they have in common. Two
> answers to "how do you run a personal agent?", standing on one substrate.

---

## What it does

### Product management (the core job)

Hermes owned the connective tissue of product work so it didn't pile up on me:

- **Captures work as tickets.** Turns a message, a voice note, a screenshot or
  a half-formed idea into a well-formed ticket with title, context and
  acceptance criteria, in one fixed schema, instead of letting it evaporate in
  a chat.
- **Triages and organizes.** Sorts incoming items, flags duplicates, keeps
  priorities and statuses sane.
- **Keeps the backlog honest.** Surfaces what's stalled, what's unclear and
  what's ready, so planning is a review, not an archaeology dig.
- **Runs the test loop.** Groups tickets that are ready for testing into short
  test sessions and records the result from a one-line reply ("ok" or "fail").
- **Drafts the product artifacts.** User stories, acceptance criteria, release
  notes: drafted for review, never shipped unattended.

### Routines (the daily rhythm)

Once the core job worked, the recurring work moved onto a schedule. Each
routine follows the same pattern: a plain script collects the facts, and a
single model call writes the summary. Cheap, predictable, and easy to debug.

- **Morning briefing** on weekdays: what's due, what's blocked, what changed.
- **Mail triage:** sorts the inbox into categories and flags what needs me.
- **Deadline watcher:** warns ahead of dates that matter.
- **Weekly review** on Friday afternoon.
- **Meeting reminder** an hour before demos, without any model at all.

### 24/7 assistant (the rest)

Because it was always up and reachable, Hermes was also a general assistant:
answering questions, fielding quick tasks and handling the small recurring
things at any hour, without me opening a laptop.

In practice Hermes managed the backlog in **Linear** and was reachable through
a **Telegram** bot, by text or voice note. Capturing a bug, filing an idea or
asking it something was just a message, from anywhere.

---

## Why always-on, self-hosted

The defining choice. A local, on-demand agent is great for focused work you
initiate. But product management is **event-driven and never stops**: a bug
gets reported at 11pm, a question lands while you're traveling. That argues for
a different shape:

| | On-demand (local) | Always-on (Hermes) |
| --- | --- | --- |
| **Lifecycle** | Runs when you summon it | Runs 24/7 as a service |
| **Trigger** | You start it | Reacts to events + you |
| **Reachability** | Your machine | Anywhere (VPS) |
| **Best for** | Focused, initiated tasks | Continuous ops, capture, monitoring |
| **Cost of ownership** | ~zero idle | A box to keep alive & secure |

Self-hosting on a VPS rather than a managed platform buys **control**: full say
over what it can touch, where data lives and how it's wired, at the price of
owning the uptime and the security. For a CEO running their own product, that
trade landed on the side of control.

See [docs/deployment.md](docs/deployment.md) for the always-on operating model
and [docs/product-management.md](docs/product-management.md) for the ticket
workflow.

---

## Keeping it alive and safe

An agent that reads untrusted content all day and runs unattended needs more
than a good prompt:

- **Sandboxed.** It works inside a restricted environment with guard rules on
  what it may run and touch, reviewed against the OWASP guidance for agentic AI.
- **Watched.** A daily health check verifies that its model access and tool
  connections actually work, and stays silent when everything is fine.
- **Self-healing.** If it stops showing signs of life, it is restarted
  automatically.
- **Accountable.** A nightly job writes a readable logbook of what it did and
  versions its configuration, so every change can be traced and rolled back.

---

## Design principles

Hermes inherits the same discipline as the rest of my agent setup:

- **Drafts, not unilateral action.** It creates and organizes tickets and drafts
  artifacts; anything that ships or goes to a person is reviewed.
- **Only confirmed facts.** Missing detail is flagged as missing, not invented.
  A vague ticket with an honest gap beats a confident wrong one.
- **Narrow, auditable scope.** It touches the systems it needs and no more, and
  every action it takes is inspectable.
- **Human in the loop on decisions.** Hermes keeps product *moving*; it doesn't
  get to *decide* product.

---

## Status & scope

A showcase, not a product. Hermes was in daily use from summer to autumn 2026
against a specific app, ticketing system and channels, on private
infrastructure, none of which is in this repo. What's here is the architecture,
the operating model and the reasoning behind running an agent as an always-on
service.

Built on an LLM agent runtime.

Shared for reference, not licensed for reuse.
