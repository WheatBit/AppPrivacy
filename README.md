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
├── giftlist/  privacy.html  + style.css   (iPhone and Android; not released yet)
├── breathe/   privacy.html  + style.css   (not released yet)
├── holibop/   privacy.html  + style.css   (not released yet)
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
permission — and make the page match. As of October 2026:

| App | Leaves the device? |
|---|---|
| BookWrite: ScribeMe | Nothing, unless the user turns on iCloud sync (their own private CloudKit database) |
| Book Tracker: Lexi | Book lookups (ISBN, title, author name, words read off spines) → Open Library, Google Books and Apple Books. Spine library and reading together → Lexi's public CloudKit database |
| DayWeaver | Nothing over the network in the current build (the optional Google connection, read-only Calendar + Tasks, isn't configured). Writes to Apple Calendar and Reminders when the user syncs or edits |
| GiftList | Store pages, fetched on the phone only when the user taps Check prices. iPhone sharing: sealed lists in the owner's private CloudKit database. `.giftlist` files the user sends |
| Breathe | Nothing. Optional events in the user's own calendar |
| HoliBop! | Nothing. No network at all |
| BlueBench | Nothing. Bluetooth only; exports go wherever the user shares them |
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
| GiftList | `https://wheatbit.github.io/AppPrivacy/giftlist/privacy.html` |
| Breathe | `https://wheatbit.github.io/AppPrivacy/breathe/privacy.html` |
| HoliBop! | `https://wheatbit.github.io/AppPrivacy/holibop/privacy.html` |

App Store Connect also asks for a **Support URL** — you can reuse the landing page
(`https://wheatbit.github.io/AppPrivacy/`) or add a dedicated support page later.

## Keeping the stylesheet copies in sync

After editing the root `style.css`:

```sh
for d in scribeme dayweaver lexi bluebench giftlist breathe holibop penna weave lunara; do cp style.css "$d/style.css"; done
```

## Adding another app

Copy an existing app folder (it already includes `style.css`), rename it, edit the
policy text, and add a link to `index.html`. Commit and push — Pages redeploys
automatically.

## Updating a policy

Edit the file, bump the "Last updated" date at the top, commit, and push.
