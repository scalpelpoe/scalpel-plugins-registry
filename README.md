# Scalpel plugins registry

The curated list of third-party plugins for [Scalpel](https://github.com/scalpelpoe/scalpel). Scalpel fetches `registry.json` from this repo's `main` branch on overlay startup and populates the in-app **Settings → Plugins → Browse** view from it.

## Submitting a plugin

1. Ship a working plugin in your own GitHub repo. See [PLUGINS.md](https://github.com/scalpelpoe/scalpel/blob/main/PLUGINS.md) in the Scalpel repo for the authoring guide and packaging requirements.
2. Tag a release on your plugin repo as `v<version>` matching your `manifest.json`'s `version`, and attach the built `plugin.js` and `manifest.json` as release assets.
3. Open a pull request against this repo adding an entry to the `plugins` array in [`registry.json`](registry.json).

## Entry schema

```json
{
  "id": "your-plugin-id",
  "name": "Display Name",
  "author": "your-github-username",
  "description": "One- or two-line description shown in the browse list.",
  "repo": "your-github-username/your-plugin-repo",
  "latestVersion": "1.0.0",
  "scalpelMinVersion": ">=0.20.0",
  "poeVersions": [1, 2],
  "iconUrl": "https://raw.githubusercontent.com/your-user/your-plugin/main/icon.png",
  "homepage": "https://github.com/your-user/your-plugin"
}
```

Fields:

- `id` - Must match `^[a-z][a-z0-9-]{2,49}$`. Identical to your plugin's manifest `id`.
- `name` / `author` / `description` - Shown in the in-app browse list.
- `repo` - Your GitHub `owner/repo`. Used to construct the release download URL.
- `latestVersion` - Matched against the installed plugin's `manifest.version`. Becomes the `v<version>` release tag.
- `scalpelMinVersion` - Comparator expression (`">=0.20.0"`). Install is blocked if the running Scalpel doesn't satisfy it.
- `poeVersions` - Optional. Omit for both PoE1 and PoE2.
- `iconUrl` - Optional. Absolute URL (usually a `raw.githubusercontent.com` path) for the row icon.
- `homepage` - Optional. Shown below the description as a repo link.

## Review

PRs are reviewed manually before merging. We confirm:

- The linked repo exists and the tagged release is reachable
- The downloaded `manifest.json` matches the registry entry's `id` and `latestVersion`
- The author isn't obviously malicious

Plugins run with full renderer privileges. Users see an install confirmation but the safety story is procedural: only install from authors you trust, the registry is curated, and updates are manual.

## Updating an entry

To publish a new version of your plugin: bump `version` in your plugin's `manifest.json`, cut a new tag, attach the artifacts to the new release, and open a PR here bumping `latestVersion`.

## License

This registry is MIT-licensed. Listed plugins are licensed independently by their respective authors.
