# Screenshots

Drop product screenshots here. They're embedded from `../README.md` using
relative paths like `screenshots/diagnose.png`.

## Naming convention

Use lowercase-hyphenated filenames that describe the view:

| Filename | What it shows | Used in README |
|---|---|---|
| `diagnose.png` | Diagnose tab with a completed probe result (matched case + IT message) | **hero** — top of README |
| `auditor-trace.png` | Expanded "match trace (auditor view)" table | "Auditable by design" section |
| `about-license.png` | About tab LICENSE card (trial / buy button) | optional, purchase-section anchor |
| `history.png` | History tab with multiple past diagnoses | optional, near "History that builds evidence" |

## Recommended capture specs

- **Resolution:** capture at the app's native 1200×800 window size, or scale
  a larger capture down to ~960 px wide max for balanced rendering in GitHub.
- **Format:** PNG (lossless; crisp text).
- **Crop:** include the full app chrome (window frame + title bar optional)
  so the product identity is clear. Trim excess desktop background.
- **Light theme** for consistency across shots (dark-theme promo can come
  later).
- **Use a realistic target** in Diagnose — `self-signed.badssl.com` triggers
  the bundled corporate-TLS-inspection case nicely.

## Where they render

- `diagnose.png` appears right under the download CTA in the landing README.
- Additional screenshots can be linked inline where referenced by the README
  copy. Add them to the table above so this file stays the source of truth.
