---
initiative: Own the Front Door. Network Re-Architecture to prepare aiR for incoming scale, giving our MCP a management strategy, protecting aiR insights from leaving the product. 
owner: Kyle Kingma, Michael Pang, Corey Wagehoft (Principal Architect)
group: Infrastructure / Cloud Services
updated: November 2026
---

# Own the Front Door. Relativity aiR Network Re-Architecture — 1-Pager

**Bottom line:** Build one governed front door for Relativity aiR and the network foundation beneath it. It lets aiR absorb 3x growth, adds ability to identify all callers within the network, lets us rate limit third-party extraction, and lays the foundation for API management of aiR's new MCP server. 

Doing nothing leads to a growth ceiling and keeps aiR's valuable insights flowing to third parties.

## Problems

Network Ceiling: 

The network can't absorb 3x aiR growth, can't identify who owns the traffic within it, and routing changes are risky. The busiest regions hit capacity limits before projected 2028 growth arrives.  This hurts internal Relativity teams' ability to scale our products, and identify if it is us or third-party callers driving the traffic.

aiR Insights Extracted from the Product: 

Third-party tools such as Deloitte's NavigAite and FTI's IQ.AI pull document text out of aiR at scale, using Relativity as cheap storage/compute while the AI value is captured in external third-party products; two consultancies account for 83% of third-party extraction, and 5.2 TB moved in one day with no way to monitor and control it. This hurts Relativity's business model, strengthening the value proposition of LSPs.



Our view: Once we can identify owners of our traffic, data extraction gets harder (keeping aiR's value stays in the product), then customers will work with Relativity directly instead of through service providers.

## Outcome
By the end of 2027, Relativity owns a network that is ready for aiR's growth, can identify who is calling within it, and keeps aiR's value in the product.

Built for growth with identifiable traffic: The internal network supports 3x aiR growth, and every request traces back to a known caller.

Data Extraction we can limit: A gateway gives Relativity the ability to rate limit third-party bulk data extraction, so aiR's insights stay in the product. Additionally, limiting large data extraction requests protects other active users' experience in the product from 'General Slowness'. 

An MCP server we can manage: The MCP server gains versioning and a management solution, so AI-agent traffic runs on a governed path supporting 100,000 strategic legal users.



## Options considered
| Option | What it delivers | Cost (eng FTEs / $) | Residual risk if we stop here |
|---|---|---|---|
| ★ Network-wide re-architecture (Recommended) | One front door, regional network hubs, and authentication and rate limiting as platform features | 6 engineer FTEs; other cost [NEEDED] | Medium. Depends on Service Auth migrating authentication and on customer change management. |
| Per-application limits (first pass, paused) | Each API team builds its own data cap, as the Object Manager team did | FTEs not tracked; about 7 months to enforce one endpoint, with 10+ endpoints across 5 teams remaining | High. Can't see traffic outside instrumented code (5.2 TB in one day went unseen), and every team rolls out on its own. |
| Do nothing | Keep today's network and entry layer | 0 engineer FTEs; no other cost | High. Growth hits the IP-capacity ceiling, and third-party extraction keeps pulling aiR's value out of the product. |


## Recommendation
**Approach:** Three stages. 

First, foundations: rebuild the trust and network backbone everything sits on.

Second, one front door: move customer traffic onto a single governed gateway, tenant by tenant, and retire the old entry layer. 

Third, edge capabilities: identify callers and enforce rate limits at the door. Guardrails run throughout so teams can change their own routing safely.

**In scope:** One governed front door for all customer traffic; regional network backbone with consolidated firewalls; caller identity established once at the door; rate limiting; API management; a separate governed path for MCP and AI-agent traffic; guardrails for service-team routing
**Out of scope:** Rate-limit thresholds and commercial terms such as metering, tiering or contract limits (decided later); low-risk access points such as Mass Export, Direct SQL scripts, AZCopy and SMB (on the CNT roadmap); Windows-based workloads that can't join the service mesh; product-team action at the edge (teams own their internal service routing)


## Risks and dependencies
- Customer disruption from new limits. The first pass caused 2 emergency exceptions in 2 weeks and left 14 accounts on deferral. Mitigation: customer communication and a deferral process before enforcement; new firewall IPs need 90 days' notice to customers.
- Authentication has to move to the new front door. Mitigation: Service Auth has it in their PAT with capacity reserved, and we count the initiative done only when they complete the migration.
- Dependencies: Service Auth (authentication migration), KISS (gateway), Container Network (backbone), Security (where rate-limit authority sits), every product team (owns internal service routing; two route sets during the transition), and a pending managed edge provider decision.

## Priority
**Call:** Must-do
**Why:** Third-party extraction was the instigator, and the MCP product strategy depends on the same network work.
