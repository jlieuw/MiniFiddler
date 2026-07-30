# Releasing

Releases publish to [nuget.org](https://www.nuget.org/packages/WirePeek) via the
[`.github/workflows/publish.yml`](.github/workflows/publish.yml) workflow, which uses
**Trusted Publishing (OIDC)** — no API key is stored in the repo.

## One-time setup

1. On nuget.org → your username → **Trusted Publishing**, add a policy:
   - **Repository Owner:** `jlieuw`
   - **Repository:** `WirePeek`
   - **Workflow File:** `publish.yml`
   - **Environment:** *(leave blank)*
2. In GitHub → repo **Settings → Secrets and variables → Actions**, add a secret
   `NUGET_USER` set to your nuget.org **username** (profile name, not your email).

(First publish of a private repo's policy is provisionally active for 7 days until the
first successful push locks it to the repo — see the nuget.org docs.)

## Cutting a release

1. Bump `<Version>` in [`WirePeek.csproj`](WirePeek.csproj) and commit.
2. Publish a **GitHub Release** (Releases → Draft a new release → create a tag like
   `v0.2.0` → Publish).

The workflow packs `WirePeek` at the release's version (the tag, minus the leading `v`)
and pushes it to nuget.org. You can also trigger it manually from the **Actions** tab
with an optional version override.
