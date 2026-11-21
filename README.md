# Emoji picker

Insert standard Unicode emoji with local search, variants, favorites, and optional shortcode suggestions.

This is an optional [Denote](https://github.com/mbianchidev/denote) plugin. Its
user guide is [guide.md](guide.md); Denote shows the same guide in
**Settings → Plugins**.

## Install

Enable **Emoji picker** from **Settings → Plugins** in Denote. Denote
downloads the release archive pinned in its built-in catalog, verifies its size
and SHA-256 digest, and only then loads the plugin in an isolated worker.

## Development

Use the Node.js version in `.node-version`.

```bash
npm ci
npm run typecheck
npm test
npm run check     # manifest, guide, and import boundaries
npm run package   # build, verify, and write .plugin-artifacts/denote.emoji-picker-<version>.tgz
```

`npm run dev` rebuilds `.plugin-dev/denote.emoji-picker.tgz` on every change. Load it
in Denote Development from **Settings → Plugins → Load local plugin archive**.
Disable the local plugin before loading rebuilt bytes with the same ID.

The build uses the [Denote plugin SDK](https://github.com/denote-io/denote-plugin-sdk)
and its `denote-plugin` command. It produces a single self-contained worker
bundle and a reproducible archive with fixed file modes, no timestamps, and LF
text. The pinned Vite and Rolldown versions keep archive bytes stable.

## Release

Published versions are immutable. To release a change:

1. Bump `version` in both `plugin.json` and `package.json`.
2. Merge to `main` with CI passing.
3. Run the **Release** workflow. It builds, verifies, and publishes
   `denote.emoji-picker-<version>.tgz` as the `v<version>` release asset.
4. Update the plugin's entry in Denote's catalog to the new release so the
   application offers it.

## History

This plugin was developed in `plugins/emoji-picker` of
[mbianchidev/denote](https://github.com/mbianchidev/denote), whose history for
this directory is preserved here. `releases.json` records every version
published from that repository, with its source commit there, original asset
URL, size, and SHA-256 digest.

[v0.1.3](https://github.com/denote-io/denote-emoji-picker/releases/tag/v0.1.3) republishes the identical archive Denote
already offers (`442a2737c78f971db58a4fb6d8405a05bf997b5475496b7986ce579e682f95d0`, 105664 bytes),
built from source commit `4e180efefe2801ac3b200c0b9915dc093990b4ff` in
mbianchidev/denote. The source in this repository is unchanged from that commit.

That archive was built against the plugin SDK as of its source commit, which
predates SDK v0.1.0. Rebuilding with SDK v0.1.0 therefore produces different
bytes; the published archive stays authoritative. CI tolerates this for
v0.1.3 only, so every later version must rebuild byte for byte.

## License

[MIT](LICENSE)
