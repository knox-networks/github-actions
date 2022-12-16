# github-actions

This repository maintains the shared Github Actions workflows and action steps for the Knox Networks organization.

## Design Notes

* **_THIS IS A PUBLIC REPOSITORY. BE VERY CAREFUL NOT TO EXPOSE SENSITIVE ORGANIZATIONAL DETAILS SUCH AS ACCOUNT_**
  **_NUMBERS, ETC. THESE ITEMS SHOULD BE PROVIDED VIA SECRETS VARIABLES AND INJECTED VIA PRIVATE CALLER WORKFLOWS._**
* It would be helpful to organize the workflows and actions within this repository by subdirectory based on associated
  tech stack. However, GitHub requires that shared workflows in remote repositories maintain the same `.github`
  directory structure as if the workflow existed in the calling repository. Therefore, the reusable actions and
  workflows in this repository must exist in the `.github/actions` and `.github/workflows` directories respectively.

## Usage

### Actions

* [build-container](./.github/actions/build-container/README.md)
* [build-helm-package](./.github/actions/build-helm-package/README.md)
* [build-helm-package-v2](./.github/actions/build-helm-package-v2/README.md)

### Workflows

* [slack-notify-workflow-invoked](./.github/workflows/slack-notify-workflow-README.md)
* [slack-notify-workflow-finished](./.github/workflows/slack-notify-workflow-README.md)

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
* Provide a README file that includes a description, usage example(s) and any design notes related to your callable
  workflows.
* Prefix workflows called from this repository with `call-`.

## Changelog

_A complete Changelog history can be found in [github-actions/CHANGELOG.md](CHANGELOG.md)._
