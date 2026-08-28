# One Word Out — content

Two published files. Everything here is read-only to the world and writable
only by the repository owner.

| File | What it is |
|---|---|
| [`content.json`](content.json) | Word packs for all eighteen languages, plus the tags and hint labels that go with them. |
| [`privacy-policy.html`](privacy-policy.html) | The privacy policy the App Store and Google Play require a public URL for. |

## How the app uses content.json

Every install of One Word Out already ships a complete copy of these words, so
the game plays fully offline and nothing waits on this file. On launch the app
fetches it in the background and, **only if its `version` is higher than the
copy already cached**, overlays the built-in words with it.

```
bundled in the app  →  cached overlay (instant, offline)  →  background refresh
```

That means new words, a fixed translation or a re-tagged category reach players
on their next launch, with no app release and no review.

A failed request is not an error. If the file is unreachable, malformed, or its
version is not newer, the app keeps the words it shipped with.

## Publishing an update

From the app repository:

```bash
npm run content:export     # writes content.json
```

Bump `version` inside the file, copy it here and push. The number must only
ever go up — the app ignores anything that is not strictly newer.

## Why this is public

It has to be: every player's phone reads it directly, with no account and no
key. Nothing here is secret. These same words are already inside the app on
every device that installs it.
