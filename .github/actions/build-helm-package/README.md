# build-helm-package Action

The `build-helm-package` GHA action builds a Helm chart package` and pushes it to the Knox S3 Helm registry.
Additionally, this action pushes a Helm chart package to Knox's legacy S3 registry which is required until a full
product migration to the AWS LZ is complete.

_This GHA action utilizes the [Helm S3 plugin](https://github.com/hypnoglow/helm-s3) and requires the helm repo to be_
_initialized prior to the usage of this GHA action._

```shell
helm plugin install https://github.com/hypnoglow/helm-s3.git
helm s3 init s3://your-bucket-name/your-repo-name
```

## Usage

```yaml
jobs:
  publish-helm-chart:
    name: Publish Helm Chart
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Publish Helm Chart
        uses: knox-networks/github-actions/.github/actions/build-helm-package@main
        with:
          aws-build-role-arn: arn:aws:iam::494949494949:role/iam-role-with-S3-access
          helm-directory: ./deploy/helm
          helm-package-name: ${{ env.RELEASE_NAME }}
          legacy-aws-build-role-arn: arn:aws:iam::505050505050:role/iam-role-with-S3-access
          legacy-helm-repo-name: stable/identity
```

## Inputs

| Variable Name               | Description                                                                                                      |
|-----------------------------|------------------------------------------------------------------------------------------------------------------|
| `aws-build-role-arn`        | (Required) IAM Role ARN to assume to publish Helm package.                                                       |
| `helm-directory`            | (Required) Directory within the current repository containing target Helm chart.                                 |
| `helm-package-name`         | (Required) Helm chart package name.                                                                              |
| `aws-region`                | (Optional) AWS Region for S3 registry access (default = `us-east-2`).                                            |
| `helm-repo-name`            | (Optional) Helm Repository name _within the Helm registry_ (default = `knox`).                                   |
| `legacy-aws-build-role-arn` | (Optional) Account IAM Role ARN to assume to publish Helm package to legacy account.                             |
| `legacy-helm-repo-name`     | (Optional) Helm repository name within legacy account registry.                                                  |
