# `cloudventures`: Global DNS

[![Build status](https://img.shields.io/github/actions/workflow/status/muhlba91/cloudventures-global-dns/pipeline.yml?style=for-the-badge)](https://github.com/muhlba91/cloudventures-global-dns/actions/workflows/pipeline.yml)
[![License](https://img.shields.io/github/license/muhlba91/cloudventures-global-dns?style=for-the-badge)](LICENSE.md)
[![](https://api.scorecard.dev/projects/github.com/muhlba91/cloudventures-global-dns/badge?style=for-the-badge)](https://scorecard.dev/viewer/?uri=github.com/muhlba91/cloudventures-global-dns)

This repository contains the Global DNS for the following domains using [octoDNS](https://github.com/octodns/octodns):

- `cloudventures.cloud`
- `kmp.eu.com`

---

## Requirements

- [mise](https://mise.jdx.dev) provides Python and the virtual environment (see [Development](#development))
- [octoDNS](https://github.com/octodns/octodns), installed with `mise exec -- pip install -r requirements.txt`

## Managing the Records

Records / Domains are structured by projects. Run the commands below from the repository root (the zone directories in each `config.yaml` are relative to it), like CI does.

### Dry-Run

To check the DNS records for changes, run:

```bash
fnox exec -- octodns-sync --config-file ./projects/<project>/config.yaml
```

### Apply

To apply the DNS records for changes, run:

```bash
fnox exec -- octodns-sync --config-file ./projects/<project>/config.yaml --doit
```

## Secrets

The secrets come from Vault through [fnox](https://fnox.jdx.dev) (`fnox.toml`, installed by mise), in CI and locally:

- **CI:** `hashicorp/vault-action` only logs in (GitHub OIDC, `exportToken`); fnox reads the values listed in `fnox.toml`.
- **Locally:** set `VAULT_ADDR`, log in with the Vault CLI, and set `FNOX_PROFILE=dev`. The `dev` profile builds Google
  Cloud credentials that impersonate the CI service account, from the machine's own key (`GCP_SOURCE_CREDENTIALS` in
  the global fnox config, `~/.config/fnox/config.toml`).

Run commands with `fnox exec -- ...`. `fnox.local.toml` (ignored by git) can override values for experiments.

---

## Continuous Integration and Automations

- [GitHub Actions](https://docs.github.com/en/actions) are linting, and verifying the code.
- [Renovate Bot](https://github.com/renovatebot/renovate) is updating GitHub Actions.

## Development

Tool versions (Python) are managed with [mise](https://mise.jdx.dev): run `mise trust` and `mise install` once, then use the usual commands (`mise exec -- pip install -r requirements.txt`). mise creates the virtual environment in `.venv`.

When the Python version in `mise.toml` changes (e.g. a Renovate update), mise does not rebuild the existing `.venv`. Recreate it and reinstall the dependencies:

```bash
rm -rf .venv && mise install && mise exec -- pip install -r requirements.txt
```
