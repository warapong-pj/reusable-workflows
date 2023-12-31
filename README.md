### reusable workflows repository

example to use workflows
```
name: Build pipeline

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
    uses: warapong-pj/reusable-workflows/.github/workflows/build-docker-image.yaml@dev
    with:
      registry: ghcr.io/${{ github.actor }}
      username: ${{ github.actor }}
      application: sample-app
      version: ${{ github.ref_name }}-${{ needs.get-version.outputs.version-tag }}
    secrets:
      password: ${{ secrets.GITHUB_TOKEN }}
```

### pipeline parameter
build-docker-image
|parameter|description|type|
|:---:|:---:|:---:|
|registry|container registry name|string|
|username|container registry username|string|
|password|container registry password|strign|
|application|container image name|string|
|version|version to tag container image|string|

scan-npm-vulnerability-assessment(no parameter)

scan-docker-image-vulnerability-assessment
|parameter|description|type|
|:---:|:---:|:---:|
|registry|container registry name|string|
|application|container image name|string|
|version|version to tag container image|string|

scan-dast
|parameter|description|type|
|:---:|:---:|:---:|
|registry|container registry name|string|
|application|container image name|string|
|version|version to tag container image|string|
|port|application port|string|

update-kubernetes-manifest-with-kustomize
|parameter|description|type|
|:---:|:---:|:---:|
|registry|container registry name|string|
|application|container image name|string|
|version|version to tag container image|string|
|environment|application environment|string|

update-kubernetes-manifest-with-helm
|parameter|description|type|
|:---:|:---:|:---:|
|registry|container registry name|string|
|application|container image name|string|
|version|version to tag container image|string|
|environment|application environment|string|
