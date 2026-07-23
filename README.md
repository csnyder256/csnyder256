# Cade

I build systems that have to be right when nobody is watching: trading research that refuses to
flatter itself, tooling that a non-technical person can run without help, and products that act
on what they observe instead of just reporting it.

Most of what I enjoy is measurement. It is easy to build something that looks like it works.
The interesting engineering is in the apparatus that would tell you if it did not.

## Projects

| Project | What it does |
| --- | --- |
| [shadow-options-trading-lab](https://github.com/csnyder256/shadow-options-trading-lab) | Runs about 20 options strategies against live market data and never places an order. Records every hypothetical fill under worst, base, and optimistic cost assumptions, then grades each strategy with anytime-valid e-processes so nightly checking stays statistically legitimate. |
| [option-contract-grader](https://github.com/csnyder256/option-contract-grader) | The valuation half of the same problem, standalone. Solves implied volatility and Greeks from Black-Scholes-Merton rather than trusting vendor numbers, then scores and letter-grades every contract in a chain. |
| [ux-struggle-detector](https://github.com/csnyder256/ux-struggle-detector) | Maps a customer's web app, watches real users through a drop-in script tag, detects 40 named struggle patterns server-side, and returns help in the same HTTP response the events arrived in. |
| [grain-bids-to-excel](https://github.com/csnyder256/grain-bids-to-excel) | Built for one person doing one tedious job. Scrapes grain elevator cash-bid pages that share no common format, normalizes them into one schema, and produces the Excel workbook they used to retype by hand. |
| [gba-rom-hack-ide](https://github.com/csnyder256/gba-rom-hack-ide) | A local web IDE for Game Boy Advance ROM hacking. Scans a decompilation project into one typed manifest, edits it visually or in plain English, and builds a playable ROM. Tooling only, no game data included. |
| [RAG-OS](https://github.com/csnyder256/RAG-OS) | A blueprint, not an application. It describes how to build a self-hosted personal AI operating system: a zero-context kernel that stays running, a git-Markdown knowledge base you can audit, and dispatch of coding tasks across your own repositories. You paste it into a coding agent and it builds the system with you, stopping to ask at every design fork. Ships a runnable stdlib-only starter for the first two milestones. |
| [org-memory-os](https://github.com/csnyder256/org-memory-os) | The organizational sibling of RAG-OS: one shared, permission-aware, auditable AI memory that any number of employees use through their own agents, with the same compaction and degradation-avoidance discipline underneath. It keeps the parts of the personal design that survive a crowd and replaces the parts that do not, the single writer, the one trusted operator, and never-delete, which is right for knowledge and illegal for personal data the moment erasure applies. Thirteen pillars, seventy decision forks left open, and no starter by design. |

The first two are a pair. One decides what a contract is worth; the other runs and grades
strategies that act on that kind of judgment.

RAG-OS and org-memory-os are the odd pair, and they are meant to be. The rest of this list is
software I built; those two are the architecture written down, with the decision forks left open
instead of resolved for you. One is the always-on agent I run on my own hardware; the other is
what it has to become before a whole organization can share it without leaking it, poisoning it,
or letting it rot. Both came out of collecting the failure modes worth designing against rather
than guessing at them.

## A few things I am proud of

The two AI memory systems above are the work I am proudest of, for the same reason as everything
else here: what makes them worth anything is the apparatus that would catch them lying.

- In RAG-OS, security enforcement that is proven to fire rather than trusted. The agent
  framework's own permission callback silently never ran, so a fenced read leaked; enforcement
  moved to a hook that fires on every single tool call, and a nightly canary re-proves the
  crown-jewel paths still deny by reading a real denial back out of the audit log.
- In org-memory-os, a cross-tenant isolation canary that is a hard release gate. Every night it
  plants a unique marker in each team's memory and tries to read another team's marker back
  through the real retrieval path, and it fails the build if that ever succeeds. A shared index
  is a design claim until that probe turns it into a measured fact.
- A test in the trading repo that spawns a clean subprocess and asserts no order-placement code
  is even reachable from the live decision path. Inside a shared test process the same check
  would pass vacuously, and the test says so in a comment.
- A scraper that decides whether a column is basis or net change by testing it against the
  arithmetic identity `basis == cash - futures` across the rows, instead of guessing from the
  header text.
- An implied volatility solver that returns nothing when there is no root, rather than a
  plausible-looking lie.
- A struggle detector that hydrates prior session history before running its rules, because the
  patterns worth catching play out across several requests and a batch-local detector would
  quietly only ever fire the easy ones.

## Working notes

Every repo here is MIT licensed and has a short landing page under its About link. Where a repo
has a test suite, the count in its badge comes from CI rather than from me. Where something is
unfinished or unproven, the README says so.
