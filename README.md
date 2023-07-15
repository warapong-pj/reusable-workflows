### reusable workflows repository

example to use workflows
```
name: Build pipeline

on:
  push:
    branches:
      - dev

jobs:
  build-pipeline:
    uses: warapong-pj/target-repo/.github/workflows/docker.yaml@main
    with:
      registry: ghcr.io/warapong-pj
      application: sample-app
      version: ${{ github.ref_name }}-${{ github.sha }}
```
