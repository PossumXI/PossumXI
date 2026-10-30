<p align="center">
  <img src="https://aura-genesis.org/brand/arobi-technology-alliance.jpeg" alt="Arobi Technology Alliance, Inc." width="780" />
</p>

# Gaetano Comparcola

**Founder & CEO, Arobi Technology Alliance, Inc. · Superintelligence researcher.** I build AI that can show its work: agents and machines that act only with current authority and leave evidence that anyone can check afterwards.

[Ullumii](https://www.iorch.net/ullumii) · [Download](https://aura-genesis.org/download) · [HUE](https://aura-genesis.org/hue) · [Benchmarks](./BENCHMARKS.md) · [Live status](https://www.iorch.net/status) · [Company](https://aura-genesis.org/)

> **Intelligence is not authority.** A system should be able to show who was allowed to act, under which policy, what actually happened, and what evidence supports the result.

## Shipped and live (checked 2026-10-29)

| Product | What it is | Where |
|---|---|---|
| **Ullumii Cloud** | AI workspace in the browser. Free to start; paid tiers from $24/mo. | [iorch.net/ullumii](https://www.iorch.net/ullumii) |
| **Ullumii Desktop** | Signed desktop app for Windows and Linux, with auto-updates and a built-in browser that agents can use when you approve it. | [Download](https://aura-genesis.org/download) |
| **HUE** 2.2.6 | Terminal agent for Windows, Linux and macOS (Apple silicon). Signed builds with published SHA-256 checksums. | [aura-genesis.org/hue](https://aura-genesis.org/hue) |
| **Q** | The AI inside Ullumii that answers and does the work. Answers stream, with the first words in 1.0 to 1.6 s. | [Status](https://www.iorch.net/status) |
| **Immaculate** | Checks each consequential action against current authority and policy before it runs. If the check can't pass, the action doesn't run. | [iorch.net/immaculate](https://www.iorch.net/immaculate) |
| **LaaS + Verifier** | Sealed evidence records for decisions and effects, plus a verifier that recomputes them on its own. | [LaaS](https://aura-genesis.org/laas) · [Verifier](https://www.iorch.net/verifier) |
| **Arobi Network** | A live production chain that anchors evidence. It has over 1.57 million blocks and 1,630 redacted receipts anyone can inspect. | [Readiness benchmark](https://aura-genesis.org/benchmarks/arobi-spine) |
| **Whisper** | End-to-end encrypted messaging. | [aura-genesis.org/whisper](https://aura-genesis.org/whisper) |

The public status page lists 7 production services: Cloud, Q, Immaculate, the agent browser, Desktop updates, Arobi Network and evidence records. All 7 reported working on 2026-10-29.

## Benchmarks (measured, dated, method published)

Full tables, settings and limits are in **[BENCHMARKS.md](./BENCHMARKS.md)**. These are the highlights:

| Benchmark | Result |
|---|---|
| **Rubik's cube, tool-assisted orchestration** (2026-10-20) | **Ullumii solved 8 of 8** scrambles from depth 3 to depth 12, with 0 invalid moves. It used about **2,000 tokens per game**, 2 or 3 model calls, and a median of 3.9 s per game. |
| **Rubik's cube, frontier models reasoning move by move** (2026-10-18/19) | Codex solved 8 of 8 using 181k to 917k input tokens per game. Claude Code solved 3 of 4 before its preset plan-usage cap. |
| **Visual reasoning, held out** (2026-10-17) | **85%** (51 of 60), 95% interval 74–92%. Charts, receipts, tables, grids, geometry and settings screens were all 6 of 6. Each answer cost about $0.0001 (median 5.2 s). |
| **Q response latency** (2026-10-18) | First visible word in **1.0–1.6 s** with streaming. A buffered answer on the same day took 17.4 s. |
| **Arobi readiness benchmark** (live) | **100/100**: 8 of 8 public probes pass and 0 fail. The probes cover the chain, receipts, seal, replay, policy gates, entitlement and checkout. |

Every benchmark was preregistered or run on a fixed game set, scored by fixed rules, and logged per run. Where a result is negative or doesn't support a claim, we say so. See *What we don't claim* in BENCHMARKS.md.

## Research practice

- **Prereg first.** We write down the hypotheses, thresholds and held-out seeds before the first model call. Deviations are appended, never edited away.
- **Find what works by elimination.** In the vision study, 6 popular prompting techniques and 2 tools were each tested against a preset bar. None cleared it, so none shipped.
- **Honest comparisons.** Every subject plays the same games under its own published plan. A tool-assisted result is labelled as tool-assisted and never shown as the same task as move-by-move reasoning.
- **Replays are checked.** Every benchmark clip is rebuilt from the engine log and checked state by state. If a single frame mismatches, the clip is deleted.

## Engineering principles

- Authority before effect; evidence after effect.
- Current authorization beats remembered permission.
- Material change requires revalidation; human hold where required.
- Exactly-once protection where duplicate physical or financial effects matter.
- Preserve failures, contradictions and inconclusive results.
- Independent recomputation instead of trusting a dashboard.
- Nothing mocked, placeholder or hardcoded is ever presented as production proof.

## Stack

TypeScript / Node.js, Rust, Python and Go. Cloudflare Workers, Netlify, Postgres and Substrate. Cryptographic evidence, policy enforcement, agent harnesses, model routing, memory and context systems, signed desktop releases, and robotics assurance.

## About the source

All Arobi source code is proprietary to **Arobi Technology Alliance, Inc.**, and its repositories are private. This profile shows what is public: shipped products, live endpoints and measured results. Interested in a pilot, a partnership or an investment? Start at [aura-genesis.org](https://aura-genesis.org/).

## Evidence boundary

Arobi is not an insurer. No repository, benchmark, demo or public page is a safety certification or an independent third-party certification. Read each claim together with its date, method and stated limits.
