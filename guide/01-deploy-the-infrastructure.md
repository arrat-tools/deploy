<div align="center"><a name="readme-top"></a></div>

<!-- SHIELD GROUP -->
<div align="center">

[![][installation-shield]][installation-link]
[![][license-shield]][license-link]

</div>

<h1 align="center">01. Deploying the Pipeline and Infrastructure</h1>

**💡 Hint:** We recommend following guides for local development and updates through the original [repository][link-to-repo] to avoid potential misconfiguration.

## 🚀 AWS CloudFormation Deployment Template

This repository contains AWS CloudFormation templates and automation scripts to provision and manage cloud infrastructure consistently.



## 📁 Project Structure

```
.
├── template.yaml         # Main CloudFormation template
├── parameters.json       # Optional: Parameter overrides
├── deploy.sh             # Shell script to deploy the stack
├── .github/workflows/    # GitHub Actions CI/CD workflows
└── README.md             # Documentation
```



## 🖼️ Architecture Diagram

> _Replace the image link below with an actual architecture diagram._

![Architecture Diagram](https://via.placeholder.com/800x400?text=Architecture+Diagram)



## ⚙️ Prerequisites

Ensure you have the following:

- AWS CLI installed and configured  
  👉 [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- AWS credentials configured (`~/.aws/credentials`)
- Permissions to create and manage CloudFormation stacks
- Bash (for running `deploy.sh`)
- Optional: GitHub Actions secrets set up (see CI/CD section)



## ✅ Validate the Template

Before deploying:

```bash
aws cloudformation validate-template --template-body file://template.yaml
```



## 🚀 Deploying the Stack

### Option A: CLI Deployment

```bash
aws cloudformation deploy \
  --template-file template.yaml \
  --stack-name my-stack-name \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameter-overrides file://parameters.json
```

### Option B: Run the Deploy Script

Make the script executable:

```bash
chmod +x deploy.sh
```

Then run:

```bash
./deploy.sh
```



## 📡 Monitor Stack

To check deployment progress or stack outputs:

```bash
aws cloudformation describe-stacks --stack-name my-stack-name
```

Or use the [AWS CloudFormation Console](https://console.aws.amazon.com/cloudformation/).



## 🧹 Cleanup

To delete the stack and all associated resources:

```bash
aws cloudformation delete-stack --stack-name my-stack-name
```



## 🤖 CI/CD with GitHub Actions

This project includes a GitHub Actions workflow for automatic validation and deployment.

### 📂 `.github/workflows/deploy.yml`

```yaml
name: Deploy CloudFormation

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v3

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Validate Template
        run: aws cloudformation validate-template --template-body file://template.yaml

      - name: Deploy Stack
        run: |
          aws cloudformation deploy \
            --template-file template.yaml \
            --stack-name github-ci-stack \
            --capabilities CAPABILITY_NAMED_IAM
```

### 🔐 Required GitHub Secrets

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`

Set these in your repository's **Settings > Secrets and variables > Actions**.



## 🌟 Best Practices

- ✅ Validate templates before deployment
- 🔐 Use IAM policies with least privilege
- 📌 Lock dependency versions and test in dev environments
- 🔁 Use GitHub Actions for continuous integration/deployment
- 🔍 Monitor resources post-deployment using CloudWatch



## 📚 Resources

- [AWS CloudFormation Docs](https://docs.aws.amazon.com/cloudformation/)
- [AWS CLI Docs](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/)
- [GitHub Actions for AWS](https://github.com/aws-actions)



## Continue to deploying the [API][up-next-link]


[![][back-to-top]](#readme-top)


<!-- Link Groups -->

[installation-link]: https://github.com/arrat-tools/infrastructure/blob/main/README.md
[installation-shield]: https://img.shields.io/badge/Docs-blue?style=flat-square&logo=readthedocs&color=3b82f6&labelColor=334155&logoColor=f5f5f5
[license-link]: https://github.com/arrat-tools/infrastructure/blob/main/License
[license-shield]: https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square&color=3b82f6&labelColor=334155
[back-to-top]: https://img.shields.io/badge/-Back_to_top-151515?style=flat-square
[link-to-repo]: https://github.com/arrat-tools/infrastructure
[up-next-link]: https://github.com/arrat-tools/deploy/blob/main/guide/02-deploy-the-api.md
