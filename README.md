# Publish image action

This GitHub Action sets up the environment to build and push Docker images to Amazon ECR. 
It automates the process of setting up QEMU, Docker Buildx, caching Docker layers, configuring AWS credentials, and performing Docker operations.

## Inputs

| Name                  | Description                                        | Required |
|-----------------------|----------------------------------------------------|----------|
| `release_tag`         | The release tag to apply to the Docker image.      | `true`   |
| `aws_account_id`      | AWS account ID where the ECR repository is hosted. | `true`   |
| `aws_role_name`       | AWS role name to assume for authentication.        | `true`   |
| `aws_region`          | AWS region where the ECR repository is located.    | `true`   |
| `aws_ecr_name`        | Name of the ECR repository.                        | `true`   |

## Example usage

To use this action in your workflow, add the following steps to your `.github/workflows` file:

```yaml
name: Build and Publish

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Build and publish docker image
        uses:  rdeak/publish-image-action@v1
        with:
          release_tag: ${{ github.ref_name }}
          aws_account_id: ${{ secrets.AWS_ACCOUNT_ID }}
          aws_role_name: ${{ secrets.AWS_ROLE_NAME }}
          aws_region: ${{ secrets.AWS_REGION }}
          aws_ecr_name: ${{ secrets.AWS_ECR_NAME }}
```


## License

This project is licensed under the terms of the MIT license.