---
initiative: Network Re-Architecture for aiR Growth and MCP (API Management)
owner: Kyle Kingma, Michael Pang, Corey Wagehoft (Principal Architect)
group: Infrastructure / Cloud Services
updated: November 2026
---

# Network Re-Architecture for aiR Growth and MCP — 1-Pager

**Bottom line:** Fund 6 engineers to build one governed front door for Relativity aiR and the network foundation beneath it. It lets aiR absorb 3x growth, identifies all callers within the network, and lets us rate limit third-party extraction. Doing nothing hits a growth ceiling and keeps aiR's value flowing to third parties.

## Problem
The network can't absorb 3x aiR growth, can't tell who is calling, and can't ship changes safely. The busiest regions hit capacity limits before projected 2028 growth arrives. Third-party tools such as Deloitte's NavigAite and FTI's IQ.AI pull document text out of aiR at scale, using Relativity as storage while the AI value is captured elsewhere; two consultancies account for 83% of third-party extraction, and 5.2 TB moved in one day with no way to monitor and control it. This hurts Relativity's business model, the internal teams counting on that growth, and the team that owns today's entry layer and carries the incidents from network changes.

Our view: if extraction gets harder and aiR's value stays in the product, customers may work with Relativity directly instead of through service providers.

## Outcome
Relativity governs who calls it and how much they take.
- One governed front door for all customer traffic, so every caller is identified
- The ability to rate limit third-party extraction, so bulk pulls can't slow customers' reviewers (targets set in requirements gathering)
- The MCP product gets API management and a governed path for AI-agent traffic, supporting 100,000 strategic legal users

## Options considered
| Option | What it delivers | Cost (eng FTEs / $) | Residual risk if we stop here |
|---|---|---|---|
| Do nothing | Keep today's network and entry layer | 0 engineer FTEs; no other cost | High. Growth hits the IP-capacity ceiling, and third-party extraction keeps pulling aiR's value out of the product. |
| Per-application limits (first pass, paused) | Each API team builds its own data cap, as the Object Manager team did | FTEs not tracked; about 7 months to enforce one endpoint, with 10+ endpoints across 5 teams remaining | High. Can't see traffic outside instrumented code (5.2 TB in one day went unseen), and every team rolls out on its own. |
| ★ Network-wide re-architecture (Recommended) | One front door, regional network hubs, and authentication and rate limiting as platform features | 6 engineer FTEs; other cost [NEEDED: see Other cost] | Medium. Depends on Service Auth migrating authentication and on customer change management. |

## Recommendation
**Approach:** Three stages. First, foundations: rebuild the trust and network backbone everything sits on. Second, one front door: move customer traffic onto a single governed gateway, tenant by tenant, and retire the old entry layer. Third, edge capabilities: identify callers and enforce rate limits at the door. Guardrails run throughout so teams can change their own routing safely.
**In scope:** One governed front door for all customer traffic; regional network backbone with consolidated firewalls; caller identity established once at the door; rate limiting; API management; a separate governed path for MCP and AI-agent traffic; guardrails for service-team routing
**Out of scope:** Rate-limit thresholds and commercial terms such as metering, tiering or contract limits (decided later); low-risk access points such as Mass Export, Direct SQL scripts, AZCopy and SMB (on the CNT roadmap); Windows-based workloads that can't join the service mesh; product-team action at the edge (teams own their internal service routing)

## Ask
**Engineer FTEs:** 6
**Other cost:** [NEEDED: firewall capacity purchase and contract position, from the Azure and software planning exercise]; [NEEDED: edge provider commercial cost]

## Risks and dependencies
- Customer disruption from new limits. The first pass caused 2 emergency exceptions in 2 weeks and left 14 accounts on deferral. Mitigation: customer communication and a deferral process before enforcement; new firewall IPs need 90 days' notice to customers.
- Authentication has to move to the new front door. Mitigation: Service Auth has it in their PAT with capacity reserved, and we count the initiative done only when they complete the migration.
- Dependencies: Service Auth (authentication migration), KISS (gateway), Container Network (backbone), Security (where rate-limit authority sits), every product team (owns internal service routing; two route sets during the transition), and a pending managed edge provider decision.

## Priority
**Call:** Must-do
**Why:** Third-party extraction was the instigator, and the MCP product strategy depends on the same network work.
