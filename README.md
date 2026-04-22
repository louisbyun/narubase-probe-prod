<div align="center">

<img src="logo.png" alt="NaruBase Probe logo" width="96" height="96" />

# NaruBase™ Probe

**The enterprise-approvable network diagnostic tool — 100% local, no cloud AI.**

When apps fail behind corporate firewalls, proxies, or TLS inspection,
Probe identifies the exact cause and produces an IT-ready message — without
ever sending your data to the cloud.

[![Version](https://img.shields.io/badge/version-1.0.0-success)](https://github.com/louisbyun/narubase-probe-prod/releases/latest)
[![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)]()
[![License](https://img.shields.io/badge/license-Proprietary-blue)]()
[![Price](https://img.shields.io/badge/pricing-TBD-0ea5e9)]()

### [⬇ Download for Windows](https://github.com/louisbyun/narubase-probe-prod/releases/latest) · [📖 Install guide](INSTALL.md)

**v1.0.0 — Early access release.** Early-access pricing is not yet enforced in-app.

</div>

---

## The problem NaruBase Probe solves

You're working from a corporate office. A SaaS tool that worked fine yesterday
suddenly won't load. Your HTTPS API calls return certificate errors. A specific
port times out but the browser works. An internal team wiki opens but an
external vendor portal doesn't.

You open a ticket. Your IT team asks **"what's broken?"** You answer **"the
app."** They ask **"which part?"** You don't know. The ticket bounces for days.

This is the daily reality in every mid-to-large enterprise running:

- **Corporate TLS inspection** (Zscaler, Bluecoat, Palo Alto, Fortinet…) that
  intercepts HTTPS and re-signs certificates with an internal CA your app
  doesn't trust.
- **Selective firewall rules** that block specific ports, regions, or
  protocols.
- **PAC / WPAD proxies** where some URLs route and some don't, without any
  clear reason to the end user.
- **Split DNS** where internal names resolve but external ones don't (or vice
  versa).
- **VPN state interactions** where apps work off-VPN but break on-VPN
  (or the opposite).

**NaruBase Probe** runs real network tests from your machine, interprets the
results against a curated case database, and writes the diagnosis in plain
language — including a copy-ready message for your IT team with the technical
details attached. All of this happens **locally**. Nothing leaves your
computer.

## Why it's different

### 🔒 100% local, by design

No cloud AI call. No telemetry. No account. No license server check-in at
runtime. The only outbound HTTP request the app makes is an optional version
check to this marketing repository on GitHub (which can be disabled); your
diagnostic data — the URLs you test, the certificates you receive, the DNS
answers you get back — **never leaves your machine**.

This is not a privacy claim bolted onto a cloud product. It's the core of the
architecture. The product literally cannot phone home with your data because
there is no code path to do so.

### 📋 Enterprise-approvable

Most "AI diagnostic tools" fail the first enterprise security review because
they either (a) require external API calls to OpenAI / Anthropic / Gemini, or
(b) run a black-box model locally with no way for auditors to understand its
reasoning.

NaruBase Probe uses **deterministic rule-based matching** against a **fully
auditable case database** — a JSON file shipped inside the application. Every
diagnosis the app produces is traceable: for any result, you can see exactly
which patterns matched, with what weights, against which probe outputs.
Security teams can review the entire decision process statically.

### 🌐 Non-expert friendly

You don't need to know what a CA is, or what "TLS 1.3" means, or how DNS
resolution works. You type in a URL. Probe tests it. If it matches a known
corporate-network failure mode, you get:

- A **plain-language explanation** of what's happening.
- A **ready-to-send IT ticket** describing the problem with the technical
  details a helpdesk needs, pre-filled in your language (English, Korean,
  Japanese).
- **Recommended remediation steps** the end user can try first.

For IT helpdesk and consultants, the same app doubles as a fast triage tool —
one click produces the same diagnostic and ticket that would otherwise take
10-30 minutes to assemble manually.

## How it works

```
┌──────────────────────────────────────────────────┐
│  Your machine (no external calls beyond target)  │
│                                                  │
│   1. You type a URL                              │
│               │                                  │
│               ▼                                  │
│   2. Probe runs real network tests               │
│      ├─ DNS resolution                           │
│      ├─ TCP connectivity                         │
│      ├─ TLS handshake + certificate chain        │
│      ├─ HTTP(S) request                          │
│      └─ System proxy detection                   │
│               │                                  │
│               ▼                                  │
│   3. Rule engine matches results against         │
│      the bundled case database                   │
│               │                                  │
│               ▼                                  │
│   4. You see:                                    │
│      ├─ What's wrong (plain language)            │
│      ├─ IT message (copy-ready)                  │
│      ├─ Remediation steps                        │
│      └─ Full audit trace                         │
└──────────────────────────────────────────────────┘
```

### Embedded Intelligence — the architectural principle

"AI knowledge without an AI call at runtime." The diagnostic intelligence is
authored at **development time**: we (and in v2.0, enterprise customers via
custom case ingestion) write structured case definitions in JSON that encode
real-world failure signatures. Those cases are compiled into the application
binary. At runtime, the app performs real network measurements and matches
their results against the case database using explicit rules. No language
model is ever invoked. No external service is ever called.

The result: a tool that **behaves like** an AI diagnostician, but qualifies
for enterprise IT approval.

## Features (v1.0)

### Probes

- **DNS** — async resolution with timing, error classification, and IPv4/IPv6
  address enumeration.
- **TLS** — TCP + handshake via `rustls`, full certificate chain capture,
  public-root-trust detection via Mozilla's `webpki-roots`. This is the core
  signal for detecting corporate TLS inspection.

Planned for v1.1+: TCP port probe, HTTP(S) with redirect chain, system proxy
detection (WinHTTP / WinINet / PAC), Windows IP Helper route introspection,
Windows CryptoAPI chain validation.

### Matcher

- Pattern operators: `equals`, `not_equals`, `contains`, `matches` (regex),
  `is_present`, `is_absent`.
- Weighted confidence scoring with `required`-pattern short-circuiting.
- Full per-pattern evaluation trace — every decision the matcher makes is
  recoverable in the UI's "auditor view".

### Case database

v1.0 ships with one case: **`corporate_tls_inspection`** — detects the
signature of a corporate TLS inspection proxy re-signing HTTPS traffic with
an internal CA. Localized in English, Korean, and Japanese.

The case DB is the central asset of the product; it expands
release-over-release. Target for v1.x is 20-50 bundled cases covering the
most common enterprise-network failure modes.

### UI

Four tabs — **Diagnose**, **History**, **Settings**, **About** — visually
consistent with [NaruBase™ Cloud](https://github.com/louisbyun/narubase-prod),
the sister product in the NaruBase desktop tool line.

### Internationalization

Case content (title, explanation, IT-ticket template, remediation steps) ships
in English, Korean, and Japanese. UI chrome is English in v1.0; full UI
localization is planned for v1.1.

## Download & install

**Windows 10 / 11 (x86_64):**

Grab the latest MSI from the [Releases
page](https://github.com/louisbyun/narubase-probe-prod/releases/latest) and
follow [INSTALL.md](INSTALL.md).

## Roadmap

| Version | Target | Focus |
|---|---|---|
| **v1.0** | **released** | DNS + TLS probes, matcher, 1 case, desktop shell |
| v1.1 | Q2 2026 | TCP + HTTP probes, proxy detection, 10+ cases, history persistence |
| v1.2 | Q3 2026 | Windows IP Helper integration, full i18n UI, settings panel |
| v1.5 | Q4 2026 | License enforcement, paid tiers, installer signing |
| v2.0 | 2027+ | Enterprise custom-case ingestion, on-premises update server |

## FAQ

**Is my data sent anywhere?**
No. The diagnostic data — your URLs, certificates, DNS answers — stays
entirely on your machine. The only outbound call the app makes is to fetch
this repository's `version.json` for update notifications, and that can be
disabled (planned v1.1 setting).

**Does it work without internet?**
Yes, for the diagnostic itself. You need network connectivity to reach the
target you're diagnosing, of course, but Probe doesn't need to phone any
service of ours to interpret the result — the case database is embedded in
the binary.

**Does it work behind corporate TLS inspection?**
That's exactly what it's built to detect. When Probe's TLS probe encounters
a chain that doesn't validate against Mozilla's public root set, that's the
signal that corporate inspection is in the path — which is the state that
causes many SaaS apps to fail. Probe flags this explicitly.

**Can I add my own custom cases?**
Not in v1.0; case bundling is compile-time only. Custom-case ingestion is on
the v2.0 roadmap for enterprise deployments.

**macOS / Linux?**
Not yet. The architecture is cross-platform-friendly, but the Windows IP
Helper / CryptoAPI / WinHTTP probes are Windows-specific and the first target
market (Korean / Japanese / European enterprise office workers) is
Windows-dominant. macOS is on the longer-term roadmap.

**How is this different from Wireshark / ping / curl?**
Those are the right tools for network engineers. Probe is the right tool for
an end user who doesn't know what a packet is but needs to describe their
problem accurately to IT. The same underlying measurements, radically
different presentation — and a case database that does the interpretation.

**Is this the same as NaruBase Cloud?**
No. [NaruBase™ Cloud](https://github.com/louisbyun/narubase-prod) is a
local-first multi-cloud server management tool. NaruBase™ Probe is a local
network-diagnostic tool. They share the **NaruBase** brand, the **aiSwingX™**
studio, and the visual design language, but they solve different problems.

## Privacy statement

NaruBase Probe is a local desktop application. It does not collect telemetry,
it has no user accounts, and it does not transmit diagnostic data.

**Outbound network traffic the app makes:**

1. **Whatever URL you explicitly ask it to diagnose** — this is the whole
   point of the tool.
2. **An optional version check** that fetches the static `version.json` file
   from this public marketing repository at
   `https://raw.githubusercontent.com/louisbyun/narubase-probe-prod/main/version.json`.
   This request contains only a standard HTTP User-Agent identifying the
   app version and platform; no user-identifying data is sent. Disabling this
   check will be possible in v1.1's Settings panel.

Nothing else.

## License

Proprietary © 2026 aiSwingX. All rights reserved.

## Contact

Louis Byun — [louisbyun](https://github.com/louisbyun) on GitHub.

For enterprise licensing, custom-case ingestion pilots, or partnership
inquiries, please open an issue on this repository or reach out via GitHub.
