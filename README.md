# AinkradCatalog

The central app catalog for the **Ainkrad** App Store. The Ainkrad host fetches
`catalog.json` from this repo (raw URL) and lists every app in it — so **adding or
updating an app needs only a change here, not a new Ainkrad host release**.

## Layout
- `catalog.json` — the catalog (schema below). Single source of truth for app store
  presentation *and* downloads.
- `screenshots/` — screenshot images referenced by `catalog.json` via raw URLs.

## `catalog.json` schema
```jsonc
{
  "schemaVersion": 1,
  "apps": [
    {
      "appID": "gitmage",                 // stable plugin id
      "displayName": "Git Mage",
      "icon": "wand.and.stars",           // SF Symbol
      "description": "short one-liner",
      "version": "v0.2.0",                // release tag shown in the store
      "apiVersion": 1,                    // host plugin API version
      "downloadURL": "https://…/gitmage.bundle.zip",
      "sha256": "…",                      // sha256 of the bundle zip (integrity check)
      "sourceRepo": "AinkradHQ/GitMage",
      "author": "Ahmed M. Elhalaby",
      "longDescription": "detail-page copy",
      "screenshots": ["https://raw.githubusercontent.com/AinkradHQ/AinkradCatalog/main/screenshots/…png"],
      "links": [{ "title": "Homepage", "url": "https://…" }]
    }
  ]
}
```

## Adding / updating an app
1. Cut the app's release (produces the `.bundle.zip`; note its `sha256`).
2. Edit `catalog.json`: add/replace the app's entry with the new `version`,
   `downloadURL`, and `sha256`, plus its presentation metadata.
3. Commit to `main`. The host picks it up on next catalog refresh — no host release.
