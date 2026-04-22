# Install NaruBase™ Probe

## Windows 10 / 11 (x86_64)

1. Download the latest **MSI installer** from the
   [Releases page](https://github.com/louisbyun/narubase-probe-prod/releases/latest).
2. Double-click the MSI to run the installer.
3. If Windows SmartScreen warns about an unverified publisher (v1.0.0 is
   unsigned pre-release), click **More info** → **Run anyway**. Authenticode
   signing is on the roadmap for v1.0.1.
4. After install, launch **NaruBase Probe** from the Start Menu.

The app appears as a standalone window with four tabs: **Diagnose**,
**History**, **Settings**, **About**.

## First diagnosis

1. Click the **Diagnose** tab (default on launch).
2. In the URL field, type the host or URL you're having trouble with, e.g.:
   - `www.example.com`
   - `https://api.example.com/health`
   - `self-signed.badssl.com` *(a public test endpoint that simulates
     corporate TLS inspection — useful for trying Probe without being
     inside a corporate network)*
3. Click **Run**.

Probe will run the DNS and TLS probes in parallel (typically under 3
seconds), match the results against the bundled case database, and show you:

- **Top matching case** with confidence percentage.
- **Plain-language explanation** of what's wrong.
- **Copy-ready IT ticket message**.
- **Recommended remediation steps**.
- Clicking **Show match trace (auditor view)** reveals the full pattern
  evaluation — every rule that was checked, what the expected value was,
  what the actual value was, and whether each pattern matched.

## System requirements

- Windows 10 version 1809 or later, or Windows 11 (any).
- 64-bit processor (x86_64 / AMD64).
- ~50 MB of disk space for the installed app.
- Outbound TCP connectivity to the targets you want to diagnose.

No admin rights are required for per-user install. No services are
installed. No scheduled tasks are created.

## Uninstall

Windows Settings → **Apps** → search for **NaruBase Probe** → **Uninstall**.

The app stores no per-user data outside the installation directory in v1.0.
History persistence (planned v1.1) will land in
`%APPDATA%\NaruBase\Probe\`, and the uninstaller will honor standard
Windows behavior — your diagnostic history stays unless you explicitly
remove it.

## Corporate deployment

For per-machine installation across a fleet, the MSI supports standard
silent-install switches:

```
msiexec /i NaruBase-Probe-1.0.0-x64.msi /quiet /norestart
```

For questions about site licensing, air-gapped update servers, or
custom-case ingestion for internal networks, see the README's
[Contact](README.md#contact) section.

## Troubleshooting

**The installer is blocked by SmartScreen.**
v1.0.0 is not yet Authenticode-signed. Click **More info** → **Run anyway**,
or distribute a hash-verified copy via your internal software management
system.

**The app can't reach its version check.**
This is harmless. The About tab will show **"Couldn't check for updates"**
but the app functions normally. Update checks use `https://raw.githubusercontent.com`
— your network may block this host. The check is optional and will be
toggleable in Settings in v1.1.

**All diagnoses say "No case matched".**
v1.0 ships with exactly one case (`corporate_tls_inspection`). If your
target doesn't trigger that specific pattern, no case will match — that's
expected behavior for v1.0, not a bug. The case database expands with each
release.

**The TLS probe fails with `tls_handshake_error` on sites that work in my
browser.**
This could be the corporate-inspection case itself — in which case it's
information, not a failure. Check the TLS probe's **Issuer CN** and
**chain.root_is_system_trusted** values on the Diagnose result page. If the
root is not in the public trust store, you are seeing corporate inspection.
