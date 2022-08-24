# github-actions

This repository maintains the shared Github Actions workflows and action steps for the Knox Networks organization.

## Design Notes

* **_THIS IS A PUBLIC REPOSITORY. BE VERY CAREFUL NOT TO EXPOSE SENSITIVE ORGANIZATIONAL DETAILS SUCH AS ACCOUNT_**
  **_NUMBERS, ETC. THESE ITEMS SHOULD BE PROVIDED VIA SECRETS VARIABLES AND INJECTED VIA PRIVATE CALLER WORKFLOWS._**
* Currently, GitHub requires that shared workflows in remote repositories maintain the same `.github` directory
  structure as if the workflow existed in the calling repository. It would be helpful to organize workflows in various
  subdirectories based on tech stack. However, reusable workflows and actions exist in `.github/workflows` and
  `.github/actions` respectively.

## Usage

* Reference workflows from this repo via `uses: knox-networks/github-actions/.github/workflows/...`.
* Prefix caller jobs in private workflows with `call-`.

```yaml
# Private workflow in another repository...
jobs:
  call-terraform-module-build:
    name: CI
    uses: knox-networks/github-actions/.github/workflows/terraform-module-build.yml@main
    with:
      aws-region: us-east-2
      apply-examples-ci: true
    secrets:
      build-role-arn: arn:aws:iam::000000000000:role/role-to-assume
```

## Workflow Development and Versioning

Since this repository contains multiple reusable workflows, etc. it is best to do any callable workflow development in
private repositories and promote them to this repo once they've been proven, iterated upon and properly parameterized
for multiple scenarios.

### Guidelines

* **_THIS IS A PUBLIC REPOSITORY. BE VERY CAREFUL NOT TO EXPOSE SENSITIVE ORGANIZATIONAL DETAILS SUCH AS ACCOUNT_**
  **_NUMBERS, ETC. THESE ITEMS SHOULD BE PROVIDED VIA SECRETS VARIABLES AND INJECTED VIA PRIVATE CALLER WORKFLOWS._**
* Since all workflows must be in the `.github/workflows` root directory, include the targeted technology stack as a
  prefix in the workflow name. For example:
  * `terraform-module-build.yml`
  * `terraform-module-release.yml`
* If a new workflow version is necessary to support new pipeline functionality, consider adding a version suffix to the
  workflow file name since we cannot version workflows independently (via repo tags). For example:
  * `terraform-module-build-v2.yml`
  * `terraform-module-release-v2.yml`

## Changelog

_A complete Changelog history can be found in [github-actions/CHANGELOG.md](CHANGELOG.md)._
