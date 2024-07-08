# `cloudventures`: Global DNS

[![Build status](https://img.shields.io/github/actions/workflow/status/muhlba91/cloudventures-global-dns/pipeline.yml?style=for-the-badge)](https://github.com/muhlba91/cloudventures-global-dns/actions/workflows/pipeline.yml)
[![License](https://img.shields.io/github/license/muhlba91/cloudventures-global-dns?style=for-the-badge)](LICENSE.md)

This repository contains the Global DNS for the following domains using [octoDNS](https://github.com/octodns/octodns):

- `cloudventures.cloud`
- `kmp.eu.com`

---

## Requirements

- [Python](https://python.org)
- [octoDNS](https://github.com/octodns/octodns)

## Managing the Records

Records / Domains are structured by projects. The following commands apply to each project folder.

### Dry-Run

To check the DNS records for changes, run:

```bash
octodns-sync --config-file ./config.yaml
```

### Apply

To apply the DNS records for changes, run:

```bash
octodns-sync --config-file ./config.yaml --doit
```

## Environment Variables

To successfully run and configure the DNS provider, you need to set a list of environment variables:

- `GOOGLE_APPLICATION_CREDENTIALS`: reference to a file containing the Google Cloud (GCP) service account credentials

---

## Continuous Integration and Automations

- [GitHub Actions](https://docs.github.com/en/actions) are linting, and verifying the code.
- [Renovate Bot](https://github.com/renovatebot/renovate) is updating GitHub Actions.
