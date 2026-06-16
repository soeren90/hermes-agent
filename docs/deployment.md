# Always-on deployment

What it actually takes to run an agent as a 24/7 service on a VPS — the
operating model, generalized. No infrastructure specifics or secrets here.

## The shift from "script" to "service"

Running an agent once is easy. Running one *continuously* is a different
discipline, because now silence is a failure: if it's down, work quietly stops
getting captured. Three things follow.

### 1. It has to stay up
The process runs under **supervision** — restarted automatically if it dies, so
a crash at 3am isn't a lost day. Uptime is treated as a feature, not luck.

### 2. It has to survive restarts
Because conversations and tickets span time, **state and memory persist** on the
host (disk/db), not in process memory. A restart resumes context instead of
forgetting it.

### 3. It has to be observable
You can't watch a 24/7 service in real time, so it has to be **inspectable after
the fact**: structured logs of what it saw and what it did, so any action can be
traced and explained. "Why did it do that?" must always be answerable.

## Security, because it's exposed

An always-on box reachable from the internet is an attack surface, so the
boring fundamentals are non-negotiable:

- **Secrets out of code.** API keys and credentials live in environment/secret
  storage on the host, never in the repo. (This repo's `.gitignore` blocks the
  usual culprits.)
- **Least privilege.** The agent gets exactly the access it needs to the
  ticketing system and channels, and no more.
- **Locked-down host.** Standard VPS hygiene — restricted access, patching,
  minimal exposed surface.

## The cost-of-ownership trade

Self-hosting is a conscious trade:

| Why self-host | What it costs |
| --- | --- |
| Full control of scope & wiring | You own the uptime |
| Control over where data lives | You own security & patching |
| No managed-platform limits | You own monitoring & recovery |
| Predictable, flat cost | It's a real box to look after |

For a personal product agent where control mattered, that trade fell on the
side of self-hosting — accepting the ops burden in exchange for owning the whole
stack.

## The takeaway

The interesting engineering in an always-on agent often isn't the prompting —
it's treating it like **production infrastructure**: supervised, persistent,
observable, and secured. That mindset is the difference between a clever demo
and something you actually trust to run your product workflow while you sleep.
