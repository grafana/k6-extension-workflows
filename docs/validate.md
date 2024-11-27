## Validate

Opinionated all-in-one workflow, fits most extensions.

![Visualization](validate-dark.png#gh-dark-mode-only)
![Visualization](validate-light.png#gh-light-mode-only)

### Usage

```yaml
name: Validate

on:
  workflow_dispatch:
  push:
    branches: ["main", "master"]
  pull_request:
    branches: ["main", "master"]

jobs:
  validate:
    name: Validate
    uses: grafana/k6-extension-workflows/.github/workflows/validate.yml@v0.1.0
```

### Inputs

Name           | Default                                                | Description
---------------|--------------------------------------------------------|--------------------
`go-versions`  |`'["1.22.x", "1.21.x"]'`                                | Go versions to use for testing and building
`platforms`    |`'["ubuntu-latest", "windows-latest", "macos-latest"]'` | Target platforms to use for testing and building
`passing-grade`|`C`                                                     | Passing compliance grade
`public`       |`public`                                                | Static content directory for GitHub Pages

### Jobs

#### Lint

Static analysis using the [golangci-lint](https://github.com/golangci/golangci-lint) linter. The version of golangci-lint will be detected using the [grafana/k6-extension-actions/golangci-lint-version](https://github.com/grafana/k6-extension-actions/tree/main/golangci-lint-version) composite action.

#### Trial

Quick test execution to detect trivial errors. This way the workflow stops with an error sooner and you don't have to wait for slower tests using multiple go versions with race detection on multiple platforms.

#### Test

Running tests on multiple platforms using multiple go versions. The list of platforms to use can be specified in the `platforms` input parameter, and the go versions to use can be specified in the `go-versions` input parameter.

#### Build

Building k6 with the extension on multiple platforms using multiple go versions and multiple k6 versions. The list of platforms to use can be specified in the `platforms` input parameter, and the go versions to use can be specified in the `go-versions` input parameter. The k6 versions will be detected using the [grafana/k6-extension-actions/k6-versions-to-test](https://github.com/grafana/k6-extension-actions/tree/main/k6-versions-to-test) composite action.

#### Compliance

Running compliance checks using [k6lint](https://github.com/grafana/k6lint). A grade of `C` or better is required by default. This can be overridden in the `passing-grade` input parameter.

#### Coverage

If `CODECOV_TOKEN` secret was passed, then generate test coverage and upload it to https://codecov.io

#### Pages

If there is a TypeScript API declaration file (`index.d.ts`) and either `tsconfig.json` or `typedoc.json`, then generate an API documentation site using [typedoc](https://typedoc.org). When running on the default branch (`main` or `master`), the generated site is also deployed using GitHub Pages.

#### Config

Generate configuration output variables for other jobs.

Variable      | Summary
--------------|--------
`k6-versions` | k6 versions to use for building k6
`go-version`  | go version to use (first item from `go-versions` input array)
`codecov`     | `true` if `CODECOV_TOKEN` secret was passed
`api-doc`     | `true` if there is a `index.d.ts` and either `tsconfig.json` or `typedoc.json`
