# `github-actions` Changelog

_The following sections summarize the changes made throughout this project and the approximate date each of the changes_
_were made._

## [12/16/2022]

* `action/build-helm-package`
  * Modified action to include functionality / inputs to publish to legacy S3 Helm registry.
  * Documentation updates.
* `action/build-helm-package-v2`
  * Action introduced from `action/build-helm-package` _without_ the functionality to publish to legacy S3 Helm
    registry.

## [12/08/2022]

* `slack-notification-workflow-invoked.yml`
  * Workflow introduced to notify corporate Slack `#development` channel of invoked workflow events.
* `slack-notification-workflow-finished.yml`
  * Workflow introduced to notify corporate Slack `#development` channel of finished workflow events.
* `action/build-container`
  * Action introduced to build container images and (if caller opts-in) pushes the image to ECR.
* `action/build-helm-package`
  * Action introduced to build Helm chart packages and publish to the corporate Helm chart registry.

## [11/21/2022]

* `terraform-root-module-build.yml`
  * Fixes missing `terraform init` call in "Terraform Plan" step.

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
