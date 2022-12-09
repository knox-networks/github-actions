# build-container Action

The `build-container` GHA action builds a container image given a `Dockerfile` and pushes the image to its ECR
repository. Each image is tagged with its corresponding GitHub commit hash as well as the `latest` tag.

## Usage

```yaml
jobs:
  container-build:
    name: Container Build
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Build Container Image
        uses: knox-networks/github-actions/.github/actions/build-container@main
        uses: ./.github/actions/build-container
        with:
          aws-build-role-arn: arn:aws:iam::494949494949:role/iam-role-with-ECR-access
          aws-ecr-repo-name: ${{ env.RELEASE_NAME }}
```

## Inputs

| Variable Name        | Description                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------|
| `aws-ecr-repo-name`  | (Required) ECR repository name.                                                                        |
| `aws-build-role-arn` | (Required) IAM Role ARN to assume for ECR-related tasks.                                               |
| `aws-region`         | (Optional) AWS Region for ECR repository access (default = `us-east-2`).                               |
| `dockerfile-path`    | (Optional) Path to target `Dockerfile` (default = `./Dockerfile`)                                      |
| `push-image`         | (Optional) Boolean indicating whether or not to push the container image to ECR (default = `"false"`). |
