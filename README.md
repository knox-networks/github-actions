# github-actions

This repository maintains the shared Github Actions workflows and action steps for the Knox Networks organization.

## Design Notes

* Currently, GitHub requires that shared workflows in remote repositories maintain the same `.github` directory
  structure as if the workflow existed in the calling repository. It would be helpful to organize workflows in various
  subdirectories based on tech stack. However, reusable workflows and actions exist in `.github/workflows` and
  `.github/actions` respectively.

## Workflow Development and Versioning

Since this repository contains multiple reusable workflows, etc. it is best to do any callable workflow development in
private repositories and promote them to this repo once they've been proven, iterated upon and properly parameterized
for multiple scenarios.

### Guidelines

* Since all workflows must be in the `.github/workflows` root directory, include the targeted technology stack as a
  prefix in the workflow name. For example:
  * `terraform-module-build.yml`
  * `terraform-module-release.yml`
* If a new workflow version is necessary to support new pipeline functionality, consider adding a version suffix to the
  workflow file name since we cannot version workflows independently (via repo tags). For example:
  * `terraform-module-build-v2.yml`
  * `terraform-module-release-v2.yml`
