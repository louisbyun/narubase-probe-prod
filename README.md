<div align="center">

<img src="logo.png" alt="NaruBase Probe" width="96" height="96" />

# NaruBase™ Probe

### Stop the IT-ticket ping-pong.

**The only AI-like network diagnostic your corporate IT will actually approve.**
100% local. No cloud. No telemetry. No accounts.

[![Version](https://img.shields.io/badge/version-1.0.0-success)](https://github.com/louisbyun/narubase-probe-prod/releases/latest)
[![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)]()
[![Price](https://img.shields.io/badge/price-%2499%20one--time-0ea5e9)]()
[![License](https://img.shields.io/badge/license-Proprietary-blue)]()

### [⬇ Download for Windows](https://github.com/louisbyun/narubase-probe-prod/releases/latest) &nbsp;·&nbsp; [📖 Install guide](INSTALL.md)

**Free during early access.** $99 one-time at v1.1. **No subscription. Ever.**

</div>

---

## "Why is this app broken?"

You know the scene. A SaaS tool that worked yesterday suddenly won't load.
An API returns certificate errors. A specific port times out. Your IT ticket
bounces for three days: *"what's broken?"* → *"the app"* → *"which part?"* →
*"I don't know."*

Meanwhile your browser keeps saying "Connection not secure" and your boss is
asking why the report isn't ready.

**NaruBase Probe tells you exactly what's wrong — in the same tab — and
writes the IT ticket for you.**

## In 10 seconds

<img src="logo.png" alt="" width="24" align="left" /> &nbsp; Paste the URL that isn't working.

<img src="logo.png" alt="" width="24" align="left" /> &nbsp; Probe runs the network tests locally.

<img src="logo.png" alt="" width="24" align="left" /> &nbsp; Read the plain-language diagnosis.

<img src="logo.png" alt="" width="24" align="left" /> &nbsp; Click **Copy IT message** — paste into your ticket.

That's it. No expertise required. No cloud service to trust. No data leaves
your machine.

## Three reasons your IT team will approve this

### 🔒 100% local. No exceptions.

No cloud AI. No telemetry. No accounts. No license server check-in. Your
diagnostic data — the URLs you test, the certificates you see, the DNS
answers you get — **never leaves your computer**.

The only outbound network request the app makes is an optional version
check against GitHub (toggle-off in Settings). That's it.

### 📋 Auditable by design

Every diagnosis Probe produces is traceable. One click shows you the exact
rules that matched, with what weights, against what measured values. Your
security team can statically review the entire case database before you
install. Nothing is hidden behind an opaque AI call — because there is no
AI call.

### 💳 One-time purchase. No subscription.

$99 once. You own it. Use it on your work laptop forever. Pricing tiers for
teams and site licenses available on request.

## Who it's for

| You are… | Probe helps you… |
|---|---|
| **An office employee** stuck behind corporate security | Describe your problem to IT in 30 seconds instead of 3 days |
| **An IT helpdesk agent** drowning in vague tickets | Triage incoming issues in seconds with a single-pane diagnostic |
| **A consultant / freelancer** hopping between client networks | Understand a new corporate environment in one run |

## What's in v1.0

- **DNS** and **TLS** diagnostic probes (more coming every release)
- Detection of the #1 enterprise blocker: **corporate TLS inspection**
  rewriting certificates with an internal CA your app doesn't trust
- Ready-to-send IT ticket messages in **English, Korean, and Japanese**
- Full auditor view of every matching rule
- Cross-version update notifications

See [CHANGELOG](https://github.com/louisbyun/narubase-probe/blob/main/CHANGELOG.md)
for the detailed scope of v1.0.0.

## Roadmap — shipping every few weeks

- **v1.1** — TCP, HTTP, and proxy probes. 10+ diagnostic cases. Local
  history persistence. Settings panel.
- **v1.2** — Windows IP Helper route introspection. Full UI localization
  (Korean / Japanese). Authenticode-signed installer.
- **v1.5** — Paid license enforcement. Team and Enterprise tiers.
- **v2.0** — Enterprise custom-case ingestion. On-premises update server
  for air-gapped deployments.

## Frequently asked

**Is my data sent anywhere?**
No. Zero diagnostic data leaves your machine. The only outbound HTTP request
is an optional version-check to this public repository.

**Will it work behind our corporate proxy / firewall / TLS inspection?**
That's exactly what it's built to detect. Probe is designed to tell you
*because* your corporate security is in the path — not *despite* it.

**Does it work offline?**
The diagnosis itself, yes. You need connectivity to whatever target you're
trying to reach, of course. But Probe doesn't call any service of ours to
interpret the result.

**How is this different from Wireshark / curl / ping?**
Those tools are for network engineers. Probe is for the other 99% of
employees — the people who have a problem but don't know what a packet is.

**macOS / Linux?**
Windows-first. Other platforms on the longer-term roadmap.

**Is this a rebrand of NaruBase Cloud?**
No. [NaruBase™ Cloud](https://github.com/louisbyun/narubase-prod) is a
multi-cloud server management tool. Probe is a network-diagnostic tool.
Same studio, same brand family, different products.

## Enterprise & team licensing

Per-seat team licensing and site licenses for enterprise deployments are
available. Contact for quotes, pilot agreements, or custom-case ingestion.

## Download

### [⬇ Latest release — Windows x64](https://github.com/louisbyun/narubase-probe-prod/releases/latest)

- **MSI installer** — for standard / silent-install deployment.
- **NSIS setup.exe** — for manual installs.

See [INSTALL.md](INSTALL.md) for walkthrough, system requirements, and
troubleshooting.

## Legal

Proprietary © 2026 aiSwingX. All rights reserved.

Source: [louisbyun/narubase-probe](https://github.com/louisbyun/narubase-probe) (private).

Contact: [Louis Byun on GitHub](https://github.com/louisbyun)
