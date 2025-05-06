# k6-extension-workflows

> [!WARNING]
> **Deprecated**. Use the reusable workflows from [xk6](https://github.com/grafana/xk6) or the [setup-xk6](https://github.com/grafana/setup-xk6) action.

Set of reusable GitHub workflows to support k6 extension development.

The workflows use composite actions from the [grafana/k6-extension-actions](https://github.com/grafana/k6-extension-actions) repository as building blocks. Using them allows for more flexibility than reusing workflows as is. However, reusing workflows is much easier and more convenient.

## Validate

Opinionated all-in-one workflow, fits most extensions.

![Visualization](docs/validate-dark.png#gh-dark-mode-only)
![Visualization](docs/validate-light.png#gh-light-mode-only)

[Details](docs/validate.md)

## Release

Workflow for creating and attaching release artifacts.

![Visualization](docs/release-dark.png#gh-dark-mode-only)
![Visualization](docs/release-light.png#gh-light-mode-only)

[Details](docs/release.md)
