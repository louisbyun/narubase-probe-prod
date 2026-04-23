# Install NaruBase™ Probe

## Windows 10 / 11 (x86_64)

1. Download the latest **MSI installer** from the
   [Releases page](https://github.com/louisbyun/narubase-probe-prod/releases/latest).
2. Double-click the MSI to run the installer.
3. Launch **NaruBase™ Probe** from the Start Menu.

The app appears as a standalone window with three tabs: **Diagnose**,
**History**, and **About**.

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
- **Plain-language explanation** of what's happening.
- **Copy-ready IT ticket message** — one click to clipboard.
- **Recommended remediation steps**.
- Clicking **Show match trace (auditor view)** reveals the full pattern
  evaluation — every rule that was checked, what the expected value was,
  what the actual value was, and whether each pattern matched.

Every run is saved automatically to the **History** tab.

## Activation

NaruBase™ Probe includes a **7-day free trial** starting on first launch.
Core single-shot diagnosis remains available forever; purchasing unlocks
continued use.

To purchase:

1. Click the **About** tab.
2. Click **Buy License — $99**. Your default browser opens the Stripe
   checkout page.
3. Complete payment. Your license key arrives by email within minutes.
4. Click **Enter License Key** in the About tab. Paste the key. Click
   **Activate**.

Activation is **fully offline** — the key is verified against an embedded
public key and stored securely in your Windows Credential Manager.

## System requirements

- Windows 10 or Windows 11.
- 64-bit processor (x86_64 / AMD64).
- Outbound TCP connectivity to the targets you want to diagnose.

No admin rights are required for per-user install. No services are
installed. No scheduled tasks are created.

## Uninstall

Windows Settings → **Apps** → search for **NaruBase™ Probe** → **Uninstall**.

Your license key can be reactivated on any future install with the same
key — keep your purchase email.

## Corporate deployment

For per-machine installation across a fleet, the MSI supports standard
silent-install switches:

```
msiexec /i NaruBase-Probe-1.1.0-x64.msi /quiet /norestart
```

For questions about site licensing, air-gapped update servers, or
custom-case ingestion for internal networks, see the README's
[Contact](README.md#contact) section.

## Troubleshooting

**The app can't reach its version check.**
This is harmless. The About tab will show **"Couldn't check for updates"**
but the app functions normally.

**All diagnoses say "No case matched".**
Run `self-signed.badssl.com` to see the corporate-TLS-inspection case
trigger. The bundled case database expands with each release; if your
specific symptom isn't covered yet, it will be soon.

**The TLS probe fails with `tls_handshake_error` on sites that work in my
browser.**
This could be the corporate-inspection case itself — in which case it's
information, not a failure. Check the TLS probe's **Issuer CN** and
**chain.root_is_system_trusted** values on the Diagnose result page. If the
root is not in the public trust store, you are seeing corporate inspection.
