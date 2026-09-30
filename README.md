# Roblox Clips Publisher - public website

Static public website (home page, Terms of Service, Privacy Policy) for the **Roblox Clips Publisher**
TikTok developer app. Plain HTML + CSS only: no frameworks, no JavaScript, no analytics, no cookies,
no external fonts or other external resources.

```
tiktok-site/
    index.html          home page
    styles.css          shared stylesheet
    terms/index.html    Terms of Service
    privacy/index.html  Privacy Policy
    README.md           this file (not needed on the live site, harmless if published)
```

All links between pages are relative (`terms/`, `../privacy/`, `../styles.css`), so the site works both at a
domain root and under a GitHub Pages project path.

## Preview locally

Opening `index.html` directly in a browser works for a quick look, but folder links like `terms/` then
open a file listing instead of the page. For an accurate preview, serve the folder over HTTP.

With Python (from this folder):

```powershell
cd C:\roblox-automation\tiktok-site
python -m http.server 8000
```

Then open:

- http://localhost:8000/
- http://localhost:8000/terms/
- http://localhost:8000/privacy/

Stop the server with `Ctrl+C`.

## Publish with GitHub Pages

Nothing has been deployed. These steps are manual.

1. Create a **public** GitHub repository, for example `roblox-clips-publisher`.
2. Put the *contents* of this folder at the root of the repository (`index.html`, `styles.css`,
   `terms/`, `privacy/`). Commit and push to the `main` branch.
3. In the repository, open **Settings > Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**, branch **main**,
   folder **/ (root)**, then click **Save**.
5. Wait for the deployment to finish (the Actions tab shows its progress). The Pages settings page then shows
   the site URL.

### Expected public URLs

For a project repository named `REPO_NAME` under the GitHub account `GITHUB_USERNAME`:

| page | URL |
|---|---|
| Home `/` | `https://GITHUB_USERNAME.github.io/REPO_NAME/` |
| Terms `/terms/` | `https://GITHUB_USERNAME.github.io/REPO_NAME/terms/` |
| Privacy `/privacy/` | `https://GITHUB_USERNAME.github.io/REPO_NAME/privacy/` |

If the repository is named exactly `GITHUB_USERNAME.github.io` (a user site), the paths sit at the domain root:

| page | URL |
|---|---|
| Home `/` | `https://GITHUB_USERNAME.github.io/` |
| Terms `/terms/` | `https://GITHUB_USERNAME.github.io/terms/` |
| Privacy `/privacy/` | `https://GITHUB_USERNAME.github.io/privacy/` |

Keep the trailing slash (`/terms/`, `/privacy/`). GitHub Pages serves `terms/index.html` at that address.

### TikTok developer portal

In the TikTok developer app settings, use:

- **Website URL:** the home page URL
- **Terms of Service URL:** the `/terms/` URL
- **Privacy Policy URL:** the `/privacy/` URL

Open all three URLs in a private browser window before submitting, to confirm they load publicly over HTTPS.

## Security

This site must never contain a TikTok Client Key, Client Secret, OAuth tokens, API keys, local file paths, or
any other secret. Everything in this folder becomes public once published.

## Keeping the policies accurate

The Privacy Policy describes the app's planned behavior: TikTok OAuth sign-in, basic account info (open_id,
avatar, display name), tokens stored locally, the `video.upload` permission, uploads only when the user starts
them, no cloud user database, no analytics or ad tracking. If the app's behavior changes, for example by
adding a server, cloud storage, analytics, or new TikTok permissions, update the policy and its
"Last updated" date **before** shipping that change.
