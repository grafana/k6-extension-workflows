## Release

Workflow for creating and attaching release artifacts.

![Visualization](release-dark.png#gh-dark-mode-only)
![Visualization](release-light.png#gh-light-mode-only)

### Usage

```yaml
name: Release

on:
  push:
    tags: ["v*.*.*"]

jobs:
  release:
    name: Release
    uses: grafana/k6-extension-workflows/.github/workflows/release.yml@v0.2.0
```

### Inputs

Name           | Default                  | Description
---------------|--------------------------|--------------------
`k6-version`   | `latest`                 | The version of k6 to be used
`go-version`   | `1.22.x`                 | The Go version to be used
`os`           | `'["linux", "windows"]'` | Target `GOOS` values
`arch`         | `'["amd64", "arm64"]'`   | Target `GOARCH` values
`with`         |                          | Additional extension modules
`cgo`          | `false`                  | Enable CGO

### Jobs

#### Build

Build k6 for the operating systems and processor architectures specified as input parameters by embedding the extension. Additional extensions can be added using the `with` input parameter.

Release artifacts are created per platform from the `k6` executable and the `LICENSE` and `README.md` files.

#### Publish

Attach the created release artifacts to the release. If the release does not yet exist (only the tag), it will be created.

#### Config

Generate configuration output variables for other jobs.
