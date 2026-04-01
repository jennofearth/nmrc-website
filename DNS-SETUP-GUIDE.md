# NMRC Website — DNS & GitHub Pages Setup Guide

## Overview

**Primary domain:** `nmreforestationcenter.org`
**Redirect domains:** `nmreforestationcenter.com`, `nmreforestation.com`, `nmreforestation.org`

The primary domain will host the site. The other three will forward to it via Namecheap's URL redirect feature. No additional hosting costs.

---

## Step 1 — Create a GitHub Repository

1. Go to [github.com](https://github.com) and sign in (or create an account).
2. Create a new **public** repository. Name it anything — e.g., `nmrc-website`.
3. Upload all files from the `NMRC Website` folder into the root of the repository.
4. Make sure `CNAME` is in the root of the repo (it already contains `nmreforestationcenter.org`).

---

## Step 2 — Enable GitHub Pages

1. In your repository, go to **Settings → Pages**.
2. Under **Source**, select **Deploy from a branch** → choose `main` → `/ (root)`.
3. Click **Save**.
4. GitHub will display the GitHub Pages URL (e.g., `https://yourusername.github.io/nmrc-website/`). Note it for Step 3.

---

## Step 3 — Configure DNS on Namecheap for `nmreforestationcenter.org`

Log in to Namecheap → **Domain List** → click **Manage** next to `nmreforestationcenter.org` → go to **Advanced DNS**.

### Delete any existing A records and CNAME for `www` before adding these.

Add the following **A records** (GitHub Pages IP addresses):

| Type | Host | Value           | TTL  |
|------|------|-----------------|------|
| A    | @    | 185.199.108.153 | Auto |
| A    | @    | 185.199.109.153 | Auto |
| A    | @    | 185.199.110.153 | Auto |
| A    | @    | 185.199.111.153 | Auto |

Add a **CNAME record** for `www`:

| Type  | Host | Value                              | TTL  |
|-------|------|------------------------------------|------|
| CNAME | www  | yourusername.github.io.            | Auto |

> Replace `yourusername` with your actual GitHub username.

---

## Step 4 — Verify the Custom Domain in GitHub Pages

Back in **GitHub → Settings → Pages**:

1. Under **Custom domain**, enter: `nmreforestationcenter.org`
2. Click **Save**.
3. Check **Enforce HTTPS** (available once DNS propagates — may take up to 48 hours).

GitHub will verify DNS and provision a free TLS certificate automatically.

---

## Step 5 — Redirect the Other Three Domains (Namecheap URL Redirect)

For each of the three secondary domains, set up a **URL Redirect** in Namecheap. No DNS record changes are needed — just the redirect.

### For each domain: `nmreforestationcenter.com`, `nmreforestation.com`, `nmreforestation.org`

1. Log in to Namecheap → **Domain List** → **Manage** the domain → **Advanced DNS**.
2. Delete any existing A records.
3. Under **Redirect Domain** (or look for a redirect/forwarding option in the dashboard), add:

   - **Subdomain:** `@` (apex)
   - **Destination URL:** `https://nmreforestationcenter.org`
   - **Redirect type:** `Permanent (301)`
   - **Include path:** Yes (if available)

4. Also add a redirect for `www`:
   - **Subdomain:** `www`
   - **Destination URL:** `https://nmreforestationcenter.org`
   - **Redirect type:** `Permanent (301)`

> **Note:** Namecheap's URL redirect feature uses their own redirect service. Visitors who go to any of the four domains will land on `nmreforestationcenter.org`.

---

## Timeline

| Step | Expected time |
|------|---------------|
| GitHub Pages live (github.io URL) | Immediate |
| DNS propagation for primary domain | 1–48 hours |
| HTTPS certificate provisioned | Within a few hours of DNS verification |
| Redirect domains active | 1–48 hours |

---

## Troubleshooting

**"Domain not verified" in GitHub Pages:**
DNS hasn't propagated yet. Wait a few hours and try again. You can check propagation at [dnschecker.org](https://dnschecker.org).

**HTTPS not available:**
GitHub requires DNS to be correctly configured before it provisions a certificate. Confirm all four A records are in place and the CNAME file in the repo contains only `nmreforestationcenter.org`.

**Redirect domains not working:**
Namecheap's URL redirect may take up to 30 minutes to activate after saving. Ensure old A records were removed before adding redirects.

---

## File Structure (for reference)

```
NMRC Website/
├── index.html          ← Homepage
├── about.html          ← About NMRC
├── research.html       ← Research & Science
├── partners.html       ← Partners & Team
├── news.html           ← News & Updates
├── CNAME               ← GitHub Pages custom domain
├── css/
│   └── styles.css
└── js/
    └── main.js
```
