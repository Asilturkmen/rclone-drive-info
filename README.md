# rclone-drive-info

Public informational pages for **Rclone-Drive**, a personal Google Cloud OAuth 2.0 client used by my own [Rclone](https://rclone.org/) installations on Windows and macOS to access my Google Drive.

Google requires an application homepage and a privacy policy before an OAuth app can be published. This repository hosts both as a static site on GitHub Pages:

| Page | File | Published URL |
| --- | --- | --- |
| Homepage | `index.html` | https://asilturkmen.github.io/rclone-drive-info/ |
| Privacy Policy | `privacy.html` | https://asilturkmen.github.io/rclone-drive-info/privacy.html |

The site is plain HTML and CSS. It has no JavaScript, backend, analytics, cookies, or external requests, and it does not perform any OAuth flow or call Google APIs. Rclone is an independent open-source project; this project is not affiliated with or endorsed by Google or the Rclone developers.

## Structure

```
index.html        Homepage
privacy.html      Privacy Policy
assets/style.css  Styles (light and dark mode via prefers-color-scheme)
assets/favicon.svg
.nojekyll         Serve files as-is, without Jekyll processing
```

All internal links are relative, so the site works under the project subpath `/rclone-drive-info/` and on a custom domain without changes.

## Deployment (GitHub Pages, deploy from branch)

1. Push to the `main` branch of `Asilturkmen/rclone-drive-info` (the repository must be public on a free plan).
2. On GitHub, open **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**, choose branch **`main`** and folder **`/ (root)`**, then **Save**.
4. Wait for the "pages build and deployment" workflow under the **Actions** tab to finish, then open the URLs above.

With the GitHub CLI authenticated, steps 2–3 can be done with:

```sh
gh api -X POST repos/Asilturkmen/rclone-drive-info/pages -f "source[branch]=main" -f "source[path]=/"
```

## Local preview

```sh
python -m http.server 8000
```

Then open http://localhost:8000/.

## Security

This repository must never contain OAuth client secrets, access or refresh tokens, or `rclone.conf`. Rclone stores those locally (`%APPDATA%\rclone\rclone.conf` on Windows, `~/.config/rclone/rclone.conf` on macOS). `.gitignore` excludes common credential file names as a safety net, but check `git status` before every commit.

## Updating the privacy policy

If the OAuth scopes or the way data is used changes, update `privacy.html` and its effective date before the change takes effect, and keep the Google Cloud consent screen in sync.
