# MUES Documentation

DocFX documentation site for the **MUES** Unity package
([MUES-Core](https://github.com/j0nes-L/MUES-Core)), deployed to Vercel at
**https://mues.nwdl.org**.

The API reference is generated automatically from the C# source of MUES-Core; the
guide pages live in [`docs/`](docs/).

---

## Local development

Prerequisites:

- [.NET SDK 9.x](https://dotnet.microsoft.com/download)
- DocFX: `dotnet tool install -g docfx`

The API reference is built from the package source, which is **not** part of this
repo. Clone it next to the docs into `_source/MUES-Core` (this path is git-ignored):

```powershell
git clone https://github.com/j0nes-L/MUES-Core.git _source/MUES-Core
```

Then build and preview:

```powershell
docfx metadata docfx.json        # generate the API metadata into api/
docfx build docfx.json           # build the static site into _site/
docfx serve _site                # preview at http://localhost:8080
```

Or do it all in one step with a live-reloading server:

```powershell
docfx docfx.json --serve
```

> If you skip the `_source/MUES-Core` clone, the guide still builds — only the API
> reference will be empty.

---

## Project layout

| Path | Purpose |
|------|---------|
| `docfx.json` | DocFX configuration (metadata + build). |
| `filterConfig.yml` | Controls which API members are included. |
| `toc.yml` / `index.md` | Site navigation and landing page. |
| `docs/` | Conceptual guide articles (edit these). |
| `api/` | Generated API reference (`*.yml` are git-ignored). |
| `.github/workflows/deploy.yml` | CI: build + deploy to Vercel. |
| `vercel.json` | Static hosting / caching headers. |
| `_source/` | Cloned package source (git-ignored). |
| `_site/` | Build output (git-ignored). |

---

## Deployment

Every push to `main` builds the site in GitHub Actions and deploys the static
output (`_site/`) to Vercel. Vercel only hosts the prebuilt files — it runs no
build itself.

### 1. Create the Vercel project

1. Create a new project in Vercel (you can import this repo or create an empty
   project — the CLI deploy doesn't rely on Vercel's own build).
2. In **Settings → General**, set **Framework Preset = Other** and leave the
   **Build Command** empty / overridden, so Vercel serves the uploaded files as-is.

### 2. Add the GitHub repository secrets

In this repo: **Settings → Secrets and variables → Actions → New repository secret**.

| Secret | Where to get it |
|--------|-----------------|
| `VERCEL_TOKEN` | Vercel → Account Settings → Tokens. |
| `VERCEL_ORG_ID` | `.vercel/project.json` after running `vercel link`, or Vercel team settings. |
| `VERCEL_PROJECT_ID` | Same `.vercel/project.json`, or the project's Settings page. |
| `MUES_CORE_TOKEN` | **Only if MUES-Core is private.** A fine-grained PAT with `Contents: read` on MUES-Core. |

> Tip: run `vercel link` locally once to generate `.vercel/project.json` and copy
> the `orgId` / `projectId` values from it.

### 3. Configure the domain

1. In the Vercel project: **Settings → Domains → Add** → `mues.nwdl.org`.
2. At the DNS provider for `nwdl.org`, add the record Vercel shows — typically:
   - `CNAME` record: `mues` → `cname.vercel-dns.com`
3. Wait for DNS to propagate; Vercel issues the TLS certificate automatically.

---

## Auto-rebuild when MUES-Core changes (optional)

To rebuild the docs whenever the package source changes, add a workflow to the
**MUES-Core** repo that dispatches an event to this repo:

```yaml
# .github/workflows/trigger-docs.yml in MUES-Core
on:
  push:
    branches: [ main ]
jobs:
  trigger:
    runs-on: ubuntu-latest
    steps:
      - name: Trigger docs rebuild
        run: |
          curl -X POST \
            -H "Accept: application/vnd.github+json" \
            -H "Authorization: Bearer ${{ secrets.DOCS_DISPATCH_TOKEN }}" \
            https://api.github.com/repos/<owner>/mues-documentation/dispatches \
            -d '{"event_type":"docs-rebuild"}'
```

`DOCS_DISPATCH_TOKEN` must be a PAT with `Contents: write` (or `repo`) access to
this documentation repo. Replace `<owner>` with the repo owner.
