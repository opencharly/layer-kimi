# kimi

Moonshot Kimi Code CLI layer for OpenCharly images.

The `kimi` candy installs the `@moonshot-ai/kimi-code` npm package globally (via
`package.json`, requiring `nodejs`), landing the `kimi` CLI on the npm global
bin path at `~/.npm-global/bin/kimi`. Kimi Code is Moonshot's AI coding agent
that runs inside the container.

`kimi --version` reports a semantic version offline, so the install and bin
wiring are verifiable without network access.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `kimi` |
| Requires | `layer-nodejs` |
| Binary | `${HOME}/.npm-global/bin/kimi` |
| npm package | `@moonshot-ai/kimi-code` |
| Install files | `charly.yml`, `package.json` |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's nested `candy:` list. In the
real box schema an image is a single `candy:` node whose body carries `base:`
**and** a nested `candy:` list (there is no box-level `base:` sibling — see
`/charly-image:image` and a live example such as
`distro-cachyos/box/comfyui/charly.yml`):

```yaml
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-kimi:v2026.243.0409'
```

After the image is built:

```bash
~/.npm-global/bin/kimi --version
~/.npm-global/bin/kimi --help
```

## Layout

- `charly.yml` — the `kimi:` candy entity: the `nodejs` require, the `check:`
  assertions, and the embedded `skill:` entity.
- `package.json` — pins the `@moonshot-ai/kimi-code` npm package.
- `CHANGELOG/` — per-CalVer release notes.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-coder:kimi` — the Moonshot Kimi Code CLI
- Runtime parent: `/charly-coder:nodejs`
- Sibling AI CLIs: `/charly-coder:claude-code`, `/charly-coder:codex`, `/charly-coder:gemini`, `/charly-coder:forgecode`
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
