# Hermes — a self-hosted, always-on product-management agent

> An LLM agent that lives on a VPS and never sleeps. It runs product management
> for an app — turning conversations and signals into tickets, keeping the
> backlog honest — and doubles as a 24/7 assistant.

Hermes is the agent I run as **CEO** to keep product moving without being the
bottleneck. Unlike a local, on-demand agent you summon from your laptop, Hermes
is a **persistent service**: it's up around the clock, reachable from anywhere,
and reacts to events on its own.

This repository is a **sanitized, generalized showcase** of that system — the
architecture and the operating model, with the specific app, company, and tools
removed. It's meant to be read, not run as-is.

> **Companion repo:** [`larry`](https://github.com/soeren90/larry) shows the
> *other* deployment model — an on-demand orchestrator running a fleet of
> specialist sub-agents locally. Hermes is the always-on, single-service
> counterpart. Together they're two answers to "how do you run a personal
> agent?"

---

## What it does

### Product management (the core job)

Hermes owns the connective tissue of product work so it doesn't pile up on me:

- **Captures work as tickets.** Turns a message, a bug report, or a half-formed
  idea into a well-formed ticket — title, context, acceptance criteria — instead
  of letting it evaporate in a chat.
- **Triages and organizes.** Sorts incoming items, flags duplicates, keeps
  priorities and statuses sane.
- **Keeps the backlog honest.** Surfaces what's stalled, what's unclear, and
  what's ready — so planning is a review, not an archaeology dig.
- **Drafts the product artifacts.** User stories, acceptance criteria, release
  notes — drafted for review, never shipped unattended.

### 24/7 assistant (the rest)

Because it's always up and reachable, Hermes is also a general assistant —
answering questions, fielding quick tasks, and handling the small recurring
things at any hour, without me opening a laptop.

In practice, Hermes manages the backlog in **Linear** and is reachable through
a **Telegram** bot — so capturing a bug, filing an idea, or asking it something
is just a message, from anywhere, at any hour.

---

## Why always-on, self-hosted

The defining choice. A local, on-demand agent is great for focused work you
initiate. But product management is **event-driven and never stops** — a bug
gets reported at 11pm, a question lands while you're traveling. That argues for
a different shape:

| | On-demand (local) | Always-on (Hermes) |
| --- | --- | --- |
| **Lifecycle** | Runs when you summon it | Runs 24/7 as a service |
| **Trigger** | You start it | Reacts to events + you |
| **Reachability** | Your machine | Anywhere (VPS) |
| **Best for** | Focused, initiated tasks | Continuous ops, capture, monitoring |
| **Cost of ownership** | ~zero idle | A box to keep alive & secure |

Self-hosting on a VPS (rather than a managed platform) buys **control**: full
say over what it can touch, where data lives, and how it's wired — at the price
of owning the uptime and the security. For a CEO running their own product, that
trade landed on the side of control.

See [docs/deployment.md](docs/deployment.md) for the always-on operating model
and [docs/product-management.md](docs/product-management.md) for the ticket
workflow.

---

## Design principles

Hermes inherits the same discipline as the rest of my agent setup:

- **Drafts, not unilateral action.** It creates and organizes tickets and drafts
  artifacts; anything that ships or goes to a person is reviewed.
- **Only confirmed facts.** Missing detail is flagged as missing, not invented —
  a vague ticket with an honest gap beats a confident wrong one.
- **Narrow, auditable scope.** It touches the systems it needs and no more, and
  every action it takes is inspectable.
- **Human in the loop on decisions.** Hermes keeps product *moving*; it doesn't
  get to *decide* product.

---

## Status & scope

A showcase, not a product. The real Hermes runs against a specific app,
ticketing system, and channels, on private infrastructure — none of which is in
this repo. What's here is the architecture, the operating model, and the
reasoning behind running an agent as an always-on service.

Built on an LLM agent runtime.

Shared for reference, not licensed for reuse.
