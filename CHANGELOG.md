# `github-actions` Changelog

_The following sections summarize the changes made throughout this project and the approximate date each of the changes_
_were made._

## [08/24/2022]

* Initial repository implementation.
* Terraform Workflows
  * `terraform-module-build.yml` -- Performs typical CI/CD tasks such as module linting, security checks and apply /
    destroy operations for `examples/ci`.
  * `terraform-module-release.yml` -- Performs module release tasks such as copying module package to S3 registry and
    tagging the git repo according to the SemVer within the `VERSION` file.
