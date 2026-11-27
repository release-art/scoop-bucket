# Release.art Scoop bucket

[Scoop](https://scoop.sh) manifests for [Release.art](https://github.com/release-art)'s
command-line tools on Windows.

## Install

If you don't have Scoop yet, install it from PowerShell (no administrator
rights needed):

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
```

Add this bucket once, then install from it:

```powershell
scoop bucket add release-art https://github.com/release-art/scoop-bucket
scoop install release-art/tf-project
scoop install release-art/proof-pdf
```

`scoop update <app>` (or `scoop update *`) keeps them current.

## Apps

| App | What it is |
| --- | --- |
| [`tf-project`](bucket/tf-project.json) | [tf-project](https://github.com/release-art/tf-project) (`tfp`): a Terraform / OpenTofu wrapper with one slot per tfvars environment, safe applies and secrets from 1Password or Azure Key Vault. Windows x86_64. |
| `proof-pdf` | [proof-pdf](https://github.com/release-art/proofpress) `verify`: holds print PDFs to PDF/X (X-1a, X-3, X-4, X-5) and prepress checks. Windows x86_64. The manifest appears with proofpress's first release that ships standalone downloads. |

The manifests install the prebuilt programs attached to each project's GitHub
release, after checking their SHA-256.

## Maintaining

Each app's manifest is `bucket/<app>.json`.

**tf-project and proof-pdf update themselves:** each project's release workflow
regenerates its manifest from the release's Windows archive and commits it as
the *Release.art workflow bot* after each stable release. Edit the project's
generator rather than the manifest, or the next release overwrites your change:
[tf-project's](https://github.com/release-art/tf-project/blob/main/bin/scoop-manifest.py),
[proof-pdf's](https://github.com/release-art/proofpress/blob/main/bin/scoop-manifest.py).

To try a manifest on Windows before merging:

```powershell
scoop install .\bucket\<app>.json
```

CI installs every manifest with Scoop on Windows for each push and pull
request, which also checks each archive's SHA-256.
