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

The first two are a pair. One decides what a contract is worth; the other runs and grades
strategies that act on that kind of judgment.

## A few things I am proud of

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

Every repo here is MIT licensed and has a short landing page under its About link. Test counts
in the badges come from CI, not from me. Where something is unfinished or unproven, the README
says so.
