# AI Agent Guidance

## Project Overview

This repo builds pre-compiled Nginx dynamic modules via GitHub Actions. No application code — only a CI workflow and documentation.

## Structure

- `.github/workflows/build-nginx-modules.yml` — CI workflow (build + release)
- `README.md` — repo documentation

## Key Concepts

- Nginx version is derived from the git tag (e.g. `v1.28.0-1` → `1.28.0-1`), or from manual input on `workflow_dispatch`.
- `NGINX_BASE_VERSION` strips the `-n` suffix for downloading the source tarball from nginx.org.
- Build matrix: `{jammy, noble}` × `{amd64, arm64}` = 4 jobs.
- Modules are compiled with `--with-compat --add-dynamic-module` against the Nginx source, not installed Nginx.
- Release is only created on tag push, not on manual dispatch.

## Rules

- Do not add modules without updating both the workflow `configure` flags and `README.md`.
- Keep version format as `x.y.z` or `x.y.z-n`. The validation step enforces this.
- Do not hardcode the Nginx version in the workflow — it must come from the tag or input.
