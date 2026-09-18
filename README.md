# codex-turn-state-registry

Plugin-store registry for [codex-turn-state](https://github.com/Jazzylol/codex-turn-state), which is private.

This repository exists because CPA fetches a plugin-store registry with a forced
`Accept: application/json`, and the GitHub contents API answers that with a
base64 metadata wrapper rather than the file itself — so the registry cannot be
served from the private repo, while release metadata and artifacts can.

`registry.json` carries no secrets: a plugin id, a name, a version and the
repository URL. Everything else stays private.

## Use it

```yaml
plugins:
  enabled: true
  store-sources:
    - "https://raw.githubusercontent.com/Jazzylol/codex-turn-state-registry/main/registry.json"
  store-auth:
    - match: "https://api.github.com/repos/Jazzylol/codex-turn-state/"
      apply-to: ["metadata", "artifact"]
      type: github-token
      token-env: "CLIPROXY_PLUGIN_STORE_TOKEN"
```

Set `CLIPROXY_PLUGIN_STORE_TOKEN` to a GitHub token with read access to the
private repository.
