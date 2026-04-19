# JWT Inspector

A lightweight, single-page tool for decoding and inspecting [JSON Web Tokens](https://jwt.io/introduction) — entirely in your browser.

**Live tool:** [https://kaymask.github.io/jwt-inspector-web/](https://kaymask.github.io/jwt-inspector-web/)

---

## What it does

Paste any JWT into the textarea and the tool instantly shows you:

| Section | Details |
|---|---|
| **Algorithm & Key Info** | `alg` and `kid` (and `typ`) from the header, called out prominently so they're easy to scan |
| **Expiry Status** | Whether the token is expired based on the `exp` claim (Unix seconds); gracefully handles tokens with no `exp` |
| **Header** | Pretty-printed, syntax-highlighted JSON |
| **Payload** | Pretty-printed, syntax-highlighted JSON |
| **Signature** | Acknowledged but intentionally not displayed or verified |

## How to use

1. Open the page (locally or via GitHub Pages — see below).
2. Paste your JWT into the text area labelled **"Paste a JWT below"**.  
   Decoding happens automatically on paste; you can also click **Decode**.
3. Read the decoded output in the cards below.
4. Click **Clear** to reset.

## Important disclaimer

> **This tool is for inspection only, not validation.**  
> It decodes the header and payload so you can read the claims. It does **not** verify the signature — it cannot tell you whether a token was legitimately signed.  
> Always verify tokens server-side with a trusted library before trusting their claims.

**No data leaves your browser.** There are no network calls, no analytics, no external scripts loaded from CDNs. Everything runs in client-side JavaScript inside your browser tab.

## Hosting on GitHub Pages

The tool is a single `index.html` file with no build step or dependencies.

To enable GitHub Pages:

1. Go to **Settings → Pages** in the repository.
2. Set the source to **Deploy from a branch**, select `main`, and choose the root (`/`) folder.
3. Click **Save**. GitHub will publish the site at `https://<owner>.github.io/<repo>/`.

## Running locally

No server needed — just open the file directly:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

Or serve it with any static file server:

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Technical notes

- Pure HTML/CSS/JavaScript — no frameworks, no npm, no build step.
- Dark-mode support via `prefers-color-scheme` media query.
- Monospace font for JSON output.
- Handles malformed JWTs (wrong number of parts, invalid Base64, non-JSON content) with a clear error message rather than crashing.
- `exp` claim is compared against `Date.now()` in the browser — be aware that clock skew between the token issuer and your machine may cause minor discrepancies.
