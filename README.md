### reusable workflows repository

example to use workflows
```
name: Build Container Image

on:
  push:
    branches:
      - dev
  pull_request:
    branches:
      - dev

jobs:
  get-version:
    runs-on: ubuntu-latest
    steps:
      - name: checkout source code
        uses: actions/checkout@v3
      - name: set short commit sha
        id: vars
        run: echo "sha_short=$(git rev-parse --short HEAD)" >> $GITHUB_OUTPUT
    outputs:
      version-tag: ${{ steps.vars.outputs.sha_short }}

  build-pipeline:
    needs: get-version
    uses: warapong-pj/target-repo/.github/workflows/docker.yaml@main
    with:
      registry: ghcr.io/warapong-pj
      application: sample-app
      version: ${{ github.ref_name }}-${{ needs.get-version.outputs.version-tag }}
```
