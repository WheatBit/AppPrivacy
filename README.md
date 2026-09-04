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
├── scribeme/  privacy.html  + style.css   (App Store: BookWrite: ScribeMe)
├── dayweaver/ privacy.html  + style.css   (App Store: DayWeaver)
├── lexi/      privacy.html  + style.css   (App Store: Book Tracker: Lexi)
├── bluebench/ privacy.html  + style.css
├── penna/     privacy.html  → redirect to scribeme/
├── weave/     privacy.html  → redirect to dayweaver/
└── lunara/    privacy.html  → redirect to lexi/
```

FlipStudy manages its own policy in its own repo
(<https://richardswheatley.github.io/FlipStudy>); the landing page links to it.

**Folder names track the current App Store name.** Three apps were renamed after
launch (Penna → BookWrite: ScribeMe, Weave → DayWeaver, Lunara → Book Tracker:
Lexi) and the policies went stale, still naming apps that no longer exist under
those names. The old folders stay as redirect stubs so URLs already filed with
Apple keep resolving — **don't delete them.**

Each app folder keeps its own copy of `style.css` (referenced as a same-directory
`style.css`, not `../style.css`). This is deliberate: Safari blocks `file://` pages
from loading a stylesheet in a parent directory, so same-directory copies let the
pages render both when opened locally and when served from GitHub Pages. **If you
edit `style.css`, copy it into every app folder** (or run the snippet at the bottom).

## Accuracy is the point

A privacy policy that says something the app doesn't do is worse than no policy.
Before editing, check the app's actual behaviour — every network call, every
permission — and make the page match. As of September 2026:

| App | Leaves the device? |
|---|---|
| BookWrite: ScribeMe | Nothing, unless the user turns on iCloud sync (their own private CloudKit database) |
| Book Tracker: Lexi | Book ISBN / search terms → Open Library and Google Books, to fill in a title and cover |
| DayWeaver | Only if the user connects a Google account: read-only Calendar + Tasks, device↔Google directly |
| FlipStudy | On-device translation by default; cloud translation (Google/Microsoft) only if a parent enables it with their own API key |

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

| App | URL |
|-----|-----|
| BookWrite: ScribeMe | `https://wheatbit.github.io/AppPrivacy/scribeme/privacy.html` |
| DayWeaver | `https://wheatbit.github.io/AppPrivacy/dayweaver/privacy.html` |
| Book Tracker: Lexi | `https://wheatbit.github.io/AppPrivacy/lexi/privacy.html` |
| BlueBench | `https://wheatbit.github.io/AppPrivacy/bluebench/privacy.html` |

App Store Connect also asks for a **Support URL** — you can reuse the landing page
(`https://wheatbit.github.io/AppPrivacy/`) or add a dedicated support page later.

## Keeping the stylesheet copies in sync

After editing the root `style.css`:

```sh
for d in scribeme dayweaver lexi bluebench penna weave lunara; do cp style.css "$d/style.css"; done
```

## Adding another app

Copy an existing app folder (it already includes `style.css`), rename it, edit the
policy text, and add a link to `index.html`. Commit and push — Pages redeploys
automatically.

## Updating a policy

Edit the file, bump the "Last updated" date at the top, commit, and push.
