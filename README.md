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
```

`scoop update tf-project` (or `scoop update *`) keeps it current.

## Apps

| App | What it is |
| --- | --- |
| [`tf-project`](bucket/tf-project.json) | [tf-project](https://github.com/release-art/tf-project) (`tfp`): a Terraform / OpenTofu wrapper with one slot per tfvars environment, safe applies and secrets from 1Password or Azure Key Vault. Windows x86_64. |

The manifests install the prebuilt programs attached to each project's GitHub
release, after checking their SHA-256.

## Maintaining

Each app's manifest is `bucket/<app>.json`.

**tf-project updates itself:** its release workflow regenerates
`bucket/tf-project.json` from the release's Windows archive and commits it as
the *Release.art workflow bot* after each stable release. Edit the generator,
[`bin/scoop-manifest.py`](https://github.com/release-art/tf-project/blob/main/bin/scoop-manifest.py),
rather than the manifest, or the next release overwrites your change.

To try a manifest on Windows before merging:

```powershell
scoop install .\bucket\tf-project.json
```

CI installs every manifest with Scoop on Windows for each push and pull
request, which also checks each archive's SHA-256.
