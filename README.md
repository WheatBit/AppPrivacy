# Methodical Enterprises — app legal pages

Public privacy policies for Methodical Enterprises LLC apps. This is the **only**
public repo; each app's source stays in its own private repo. Nothing sensitive
(keys, unreleased names, internal notes) belongs here.

Repo: <https://github.com/WheatBit/AppPrivacy>

## What's here

```
.
├── index.html            landing page linking to every policy
├── style.css             stylesheet (also copied into each app folder)
├── weave/     privacy.html  + style.css
├── bluebench/ privacy.html  + style.css
├── penna/     privacy.html  + style.css
└── lunara/    privacy.html  + style.css
```

FlipStudy is intentionally not included — it manages its own privacy policy.

Each app folder keeps its own copy of `style.css` (referenced as a same-directory
`style.css`, not `../style.css`). This is deliberate: Safari blocks `file://` pages
from loading a stylesheet in a parent directory, so same-directory copies let the
pages render both when opened locally and when served from GitHub Pages. **If you
edit `style.css`, copy it into every app folder** (or run the snippet at the bottom).

## Publishing (GitHub Pages)

1. Push this folder to <https://github.com/WheatBit/AppPrivacy> (the repo must be
   **public**).
2. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a
   branch**, pick the default branch and the `/ (root)` folder, then **Save**.
3. After a minute the site is live at:

   ```
   https://wheatbit.github.io/AppPrivacy/
   ```

## The URLs to paste into App Store Connect

Under each app's **App Privacy → Privacy Policy URL**:

| App       | URL |
|-----------|-----|
| Weave     | `https://wheatbit.github.io/AppPrivacy/weave/privacy.html` |
| BlueBench | `https://wheatbit.github.io/AppPrivacy/bluebench/privacy.html` |
| Penna     | `https://wheatbit.github.io/AppPrivacy/penna/privacy.html` |
| Lunara    | `https://wheatbit.github.io/AppPrivacy/lunara/privacy.html` |

App Store Connect also asks for a **Support URL** — you can reuse the landing page
(`https://wheatbit.github.io/AppPrivacy/`) or add a dedicated support page later.

## Keeping the stylesheet copies in sync

After editing the root `style.css`:

```sh
for d in weave bluebench penna lunara; do cp style.css "$d/style.css"; done
```

## Adding another app

Copy an existing app folder (it already includes `style.css`), rename it, edit the
policy text, and add a link to `index.html`. Commit and push — Pages redeploys
automatically.

## Updating a policy

Edit the file, bump the "Last updated" date at the top, commit, and push.
