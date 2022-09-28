# `github-actions` Changelog

_The following sections summarize the changes made throughout this project and the approximate date each of the changes_
_were made._

## [09/27/2022]

* `terraform-root-module-build.yml`
  * Workflow introduced to perform typical CI/CD tasks such as module linting, security checks and `terraform plan`
    to identify the infrastructure changes to be performed during a `terraform apply`.
* `terraform-root-module-apply.yml`
  * Workflow introduced to `terraform plan` and `terraform apply` root module infrastructure changes.
* `terraform-module-release.yml`
  * Refactored "Tag Repo with VERSION" step with more readable JS.

## [08/24/2022]

* Initial repository implementation.
* `terraform-module-build.yml`
  * Workflow introduced performing typical CI/CD tasks such as module linting, security checks and apply / destroy
    operations for `examples/ci`.
* `terraform-module-release.yml`
  * Workflow introduced performing module release tasks such as copying module package to S3 registry and
    tagging the git repo according to the SemVer within the `VERSION` file.
