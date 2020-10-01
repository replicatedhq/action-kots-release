action-kots-release
=====================

A github Action to create releases for a [Replicated KOTS](https://blog.replicated.com/announcing-kots/) application.

### Usage

An example workflow is included at [./.github/workflows/main.yml](./.github/workflows/main.yml)

```yaml
name: Create a Replicated KOTS release
on: [push]

jobs:
  create_release:
    runs-on: ubuntu-latest
    name: Create a Replicated KOTS release for this commit
    steps:
    - name: Checkout
      uses: actions/checkout@v1
    - name: Create the release
      id: test-action
      uses: replicatedhq/action-kots-release@v0.1.0
      with:
        replicated-app: 'my-great-app'
        replicated-api-token: ${{ secrets.REPLICATED_API_TOKEN }}
        yaml-dir: manfests
```

### Inputs

#### replicated-app

The application slug or ID for this application. This can be found at [vendor.replicated.com/settings](https://vendor.replicated.com/settings).

#### replicated-api-token

A Replicated API token (create one at [vendor.replicated.com](https://vendor.replicated.com/team/tokens)).

#### yaml-dir

A directory containing KOTS manifests, defaults to `./manifests`.

#### release-notes

The release notes for the promoted release, defaults to `GitHub Action release of ${GITHUB_REF} triggered by ${GITHUB_ACTOR}: [${GITHUB_SHA::7}](https://github.com/${GITHUB_REPOSITORY}/commit/${GITHUB_SHA})`. If your message includes `"` they must be shell-escaped (`\"`).

#### promote-channel

The channel to promote the release into, defaults to `${GITHUB_REF}`.

#### version

The version number to set, defaults to first 7 characters of the commit SHA.

### Limiting to specific branches or patterns

To limit which branches create releases or more advanced branch filtering, check out the [GitHub Actions docs on workflow triggers](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/events-that-trigger-workflows).
