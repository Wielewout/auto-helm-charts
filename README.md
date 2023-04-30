# Automated helm charts

This repository showcases a way to automate helm charts with GitHub Actions and Pages in a mono-repo.

## Handle chart dependencies

For helm chart dependencies the required repository needs to be added.
In case a new dependency repository is needed it should be added to `bin/add-repos`.
Otherwise the workflow will be broken as helm would be unable to build the chart dependencies.

To locally add all necessary repos:

```sh
./bin/add-repos
```

## Add a new chart

```sh
./bin/add-chart example
```

> Optionally the initial version can be provided as well (default is `0.0.0`).

> **Note**
>
> When adding a new chart, the chart releaser action will always create an initial release without release please intervening.
> This means that the automatic changelog etc. will be missing in this initial GitHub release.

## Create a release PR

Normally release please automatically creates a release pull request with the appropriate version bumps.
In case a specific version needs to be forced (e.g. when creating the first official release) a "release fixture" can be set.
Release please will then pick this up to update the PR with this version.
When merged to the main branch, the "release fixture" will automatically be removed.

```sh
./bin/create-release-pr example 1.0.0
```

# Create release branch

The workflow will automatically create a release branch when a feature release is merged (e.g. `releases/example-1.0` in case the `example` chart got bumped to `1.0.0`).
This branch will be prepared to only perform patch bumps so features could also be backported.

In case this would fail, the release branch can also be created manually:

```sh
./bin/create-release-branch example 1.0
```

> There are a few additional options that can be provided.
> Execute `./bin/create-release-branch -h` for more information.
