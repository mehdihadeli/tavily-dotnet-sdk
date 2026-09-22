# Versioning and releases

The SDK uses [Nerdbank.GitVersioning (NBGV)](https://dotnet.github.io/Nerdbank.GitVersioning/)
to calculate package and assembly versions from committed version intent and
Git history.

The release policy is single-branch GitHub Flow:

- `main` is the long-lived development branch.
- Preview, RC, and stable version changes are reviewed pull requests.
- Tags identify the exact approved commit that was published.
- CI uses a full Git checkout so NBGV can calculate version metadata.

## Version lifecycle

```text
10.0.0-preview.N -> 10.0.0-rc.N -> 10.0.0
```

The prerelease label is committed in `version.json` as `preview` or `rc`.
NBGV derives the numeric suffix from Git history. A tag identifies a version;
it does not promote a preview or RC by itself.

| State               | Action                                         | Example            |
| ------------------- | ---------------------------------------------- | ------------------ |
| Start development   | Merge a version PR                             | `10.0.0-preview.1` |
| Next preview        | Run `prepare-preview` and merge the version PR | `10.0.0-preview.2` |
| Start stabilization | Run `prepare-rc` and merge the version PR      | `10.0.0-rc.1`      |
| Publish RC          | Tag the approved commit                        | `v10.0.0-rc.1`     |
| Declare stable      | Run `prepare-stable` and merge the version PR  | `10.0.0`           |
| Publish stable      | Tag the approved commit                        | `v10.0.0`          |

## Configure version intent

The committed version lives in [`version.json`](../../version.json). The
repository accepts stable and prerelease version tags through
`publicReleaseRefSpec`.

Inspect the calculated version with:

```bash
nbgv get-version -v SemVer2
```

Use `SemVer2` as the release version. It preserves suffixes such as
`10.0.0-preview.1`; do not use `NuGetPackageVersion` for Release Drafter
metadata because normalized NuGet formats may rewrite prerelease labels.

## Prepare a preview

Install NBGV once if needed:

```bash
dotnet tool install --global nbgv
```

Create the next preview version through a pull request:

```bash
./release-version.sh prepare-preview 10.0.0
git add version.json
git commit -m "Start 10.0 preview"
git push origin <branch>
```

The helper sets the prerelease label. NBGV derives the numeric suffix from Git
history, so ordinary feature, fix, test, and documentation PRs do not require
manual numeric edits. Ordinary PRs still do not change `version.json`.

## Prepare an RC

When the release line is ready for stabilization:

```bash
./release-version.sh prepare-rc 10.0.0
git add version.json
git commit -m "Begin 10.0 release candidate"
git push origin <branch>
```

After the version PR merges, validate the exact `main` commit and create its
tag:

```bash
./release-version.sh tag
git push origin v10.0.0-rc.1
```

If another RC is needed, merge the fixes and run `prepare-rc` again. The helper
will produce `10.0.0-rc.2`.

## Prepare stable

After the RC is accepted, remove the prerelease suffix through a reviewed PR:

```bash
./release-version.sh prepare-stable 10.0.0
git add version.json
git commit -m "Declare 10.0 stable"
git push origin <branch>
```

After merge and validation:

```bash
./release-version.sh tag
git push origin v10.0.0
```

After stable publication, begin the next development line with a new preview
version PR:

```bash
./release-version.sh prepare-preview 10.1.0
```

## GitHub Actions behavior

The build workflow checks out the complete Git history, restores, builds, and
tests every pull request and `main` push. A shared version job calculates NBGV
`SemVer2` once for `main` and `v*` tags.

The publish job runs for a `-preview.` version on `main`, or for any `v*` tag.
It packs and publishes the SDK to NuGet.org, then updates the matching Release
Drafter draft. Preview merges publish a NuGet prerelease while keeping the
GitHub release as a draft. RC and stable releases publish the draft only after
their approved tag is pushed.

There is no separate Release Drafter workflow. Keeping draft creation and
publication in the single publish job avoids duplicate drafts and competing
version calculations. Published prereleases are excluded from the next stable
comparison baseline.

The documentation workflow builds `docs/` with VitePress and deploys it to
GitHub Pages after changes on `main`. Enable GitHub Pages with the GitHub
Actions source in repository settings.

## Release checklist

### Preview

1. Run `prepare-preview` and open a version PR.
2. Merge the version PR and ordinary changes.
3. Inspect `nbgv get-version -v SemVer2` when needed.
4. Publish a preview tag only when the release policy requires it.

### RC or stable

1. Run `prepare-rc` or `prepare-stable` and open the version PR.
2. Merge and test the exact `main` commit.
3. Run `./release-version.sh tag`.
4. Push the created `v*` tag.

Never rewrite `version.json` in CI. Version intent belongs in reviewed source
control changes, and every tag must come from the approved commit.
