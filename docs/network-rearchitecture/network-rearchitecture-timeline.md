---
initiative: Own the Front Door. Network Re-Architecture timeline for Relativity aiR.
owner: Kyle Kingma
group: Infrastructure / Cloud Services
updated: November 2026
---

# aiR Network Re-architecture Timeline

Milestones, go-live window, and when teams are unblocked. Objective: [OKR-18774](https://jira.kcura.com/browse/OKR-18774).

> **Windows shown below are intended for planning, not committed dates.** Dates should not be communicated as hard dates to customers; they are intended to forecast team-dependency timelines for beginning work.

Interactive version: [aiR Network Timeline (Claude artifact)](https://claude.ai/artifact/9rFrbMoUq7R1khxdxDkZR2)

## Timeline

```mermaid
%%{init: {"gantt": {"fontSize": 11, "barHeight": 26, "barGap": 6, "topPadding": 40, "leftPadding": 210, "rightPadding": 20, "sectionFontSize": 12, "numberSectionStyles": 4}}}%%
gantt
    title Dec 2026 to Sep 2027 (planning windows)
    dateFormat  YYYY-MM-DD
    axisFormat  %b %Y
    todayMarker off

    section API Gateway (kGateway) OKR-18775
    Nonprod                      :done,   gw1, 2026-12-01, 2026-12-31
    Service Auth POC             :done,   gw2, 2027-01-01, 2027-03-31
    Service Auth engage          :crit,   gw3, 2027-01-01, 2027-02-28
    Nonprod + Service Auth       :done,   gw4, 2027-04-01, 2027-05-31
    Service teams rewire         :crit,   gw5, 2027-04-01, 2027-05-31
    Prod rollout + Service Auth  :active, gw6, 2027-06-01, 2027-07-31

    section vWAN hub OKR-18800
    IaC in reg                   :done,   hub1, 2026-12-01, 2026-12-31
    Traffic to prod hub          :active, hub2, 2027-04-01, 2027-05-31
    Operating                    :active, hub3, 2027-06-01, 2027-07-31

    section Firewall consolidation OKR-18809
    Notice sent                  :crit,   fw1, 2027-01-01, 2027-01-31
    90-day window                :        fw2, 2027-02-01, 2027-04-30
    Design                       :        fw3, 2027-02-01, 2027-03-31
    Nonprod                      :done,   fw4, 2027-04-01, 2027-04-30
    Prod rollout                 :active, fw5, 2027-06-01, 2027-07-31

    section DNS and hostnames OKR-18776
    Hostnames and hairpin removal :active, dns1, 2027-07-01, 2027-09-30

    section Go-live window
    Hub + firewall + kGateway    :active, golive, 2027-06-01, 2027-07-31
```

Bar labels are abbreviated to fit the windows; the tables below carry the full wording. Red bars are where another team has to engage, blue bars are production or live windows, grey bars are nonprod or deliverable windows, plain bars are design or waiting windows.

## Windows by initiative

| Initiative | Dec 2026 | Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep |
|---|---|---|---|---|---|---|---|---|---|---|
| **API Gateway (kGateway)** [OKR-18775](https://jira.kcura.com/browse/OKR-18775) | Nonprod gateway | Service Auth POC and integration | ← | ← | Nonprod live, Service Auth fully integrated | ← | **Production rollout** with Service Auth integration | ← | | |
| **vWAN hub architecture** [OKR-18800](https://jira.kcura.com/browse/OKR-18800) | IaC in regression | | | | Traffic moves to production hub | ← | **Operating** | ← | | |
| **Firewall consolidation** [OKR-18809](https://jira.kcura.com/browse/OKR-18809) | | Customer comms: reserve addresses, send 90-day notice | Consolidation design · notice window | ← | Nonprod rollout · 90-day notice window complete | | **Production rollout**, alongside the hub | ← | | |
| **DNS and hostname resolution** [OKR-18776](https://jira.kcura.com/browse/OKR-18776) | | | | | | | | **Hostname resolution and hairpin removal**, after kGateway is live | ← | ← |

**Go-live window: June and July 2027.** The hub, firewall consolidation and kGateway production rollouts land together.

## Teams to engage, and when

| When | Team | Why |
|---|---|---|
| January 2027 | Service Auth | Unblocked for early POC once the gateway is in nonprod. |
| January 2027 | Customer comms | Reserve the per-region public address range and send the 90-day customer notice; the window completes in April, ahead of the June–July production rollout. |
| April–May 2027 | Service-owning teams | Begin rewiring services to internal names against the nonprod gateway with Service Auth integrated. |
| June–July 2027 | Service Auth | Production rollout of kGateway with Service Auth integration. |
