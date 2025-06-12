<h1 align="center">Prerequisites Before Deploying ARRAT</h1>

You will need the following technologies to successfully deploy your system to AWS.

## AWS CLI

> \[!TIP]
>
> Learn the most up to date steps to set up the [AWS CLI][docs-aws-cli-download-link] by checking it out.

**🚨 Remember:** Configure your profile locally following this [guide][docs-aws-profile-setup-link]. This will be used in the coming steps when deploying templates.

### AWS SAM CLI

After following the prerequisites, download the [AWS SAM CLI][docs-aws-sam-cli-download-link] used to run and deploy AWS SAM templates.

## Nodejs / pnpm

> \[!TIP]
>
> Learn the most up to date steps to set up [Node.js][docs-nodejs-download-link] by checking it out.

_Once installed, run the following command to download `pnpm`:_

<div align="center">

  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="/images/install-pnpm-command.png">
    <img height="240" src="/images/install-pnpm-command.png" alt="Install command for pnpm using npm">
  </picture>

</div>

## Docker

> \[!TIP]
>
> Learn the most up to date steps to set up [Docker][docs-docker-download-link] by checking it out.

## Requesting GPU Access from AWS

This repository provides guidance and templates for requesting GPU-based EC2 instances from AWS, including best practices, IAM policies, request steps, and usage tips.

### Overview

Amazon Web Services (AWS) offers GPU-enabled EC2 instances for compute-intensive workloads. This guide focuses on the `g4dn.xlarge` instance, suitable for lightweight ML inference and GPU acceleration tasks.

#### Why g4dn.xlarge?

The `g4dn.xlarge` instance type is ideal for:
- Running machine learning inference tasks (e.g., PyTorch, TensorFlow).
- GPU acceleration for compute or rendering workloads.
- Development and testing with modest GPU requirements.

| Instance Type | GPU         | Memory | vCPUs | Storage  |
|---------------|-------------|--------|-------|----------|
| g4dn.xlarge   | 1x NVIDIA T4| 16 GB  | 4     | 125 GB NVMe SSD |

[🔍 g4dn Instance Details](https://aws.amazon.com/ec2/instance-types/g4/)

### Prerequisites

- AWS account with EC2 and Service Quotas permissions.
- Region selection (e.g., `us-east-1`).
- Project justification for requesting access.

### How to Request Access

#### Step 1: Check Your Service Quotas

Visit the [AWS Service Quotas Console](https://console.aws.amazon.com/servicequotas/) and search for:
- `Running On-Demand G and VT Instances`

- ![image](https://github.com/user-attachments/assets/0dd994fb-6c09-4d84-b2d8-5ed956aad835)

![image](https://github.com/user-attachments/assets/89aa77ae-041b-4226-8c0d-b00147fd12d2)


Check the current quota for your region.

#### Step 2: Submit a Limit Increase

1. Go to [AWS Service Quotas Console](https://console.aws.amazon.com/servicequotas/).
2. Locate `Running On-Demand G and VT Instances`.
3. Select your region (e.g., `us-east-1`).
4. Click **Request quota increase**.
5. Specify the number of instances you need (e.g., 1 or 2).
6. Use the justification template below.

### Sample Justification Template

```text
We are developing data processing workloads for [insert project name].
We require g4dn.xlarge instances to enable GPU acceleration and optimize model performance.
Initial usage will be limited to 1-2 instances with future scaling depending on success.

Please grant access to run 2 g4dn.xlarge instances in the us-east-1 region.
```

### Setting Up Your Instance (NVIDIA Drivers)

To use the GPU on a `g4dn.xlarge` instance, install the NVIDIA drivers and CUDA libraries.

#### Ubuntu Setup

```bash
# Update and install
$ sudo apt update
$ sudo apt install nvidia-driver-510 nvidia-utils-510
$ sudo reboot

# Confirm installation
$ nvidia-smi
```

### Best Practices

- **Tag instances** with project metadata for easier tracking.
- **Monitor GPU utilization** using `nvidia-smi` and CloudWatch.
- **Use Auto Stop/Start** schedules to reduce idle costs.

### Resources

- [EC2 Pricing](https://aws.amazon.com/ec2/pricing/)
- [Amazon EC2 Spot Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html)
- [Installing NVIDIA Drivers on EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-nvidia-driver.html)

### IAM Permissions

Ensure your IAM role or user has these permissions:
```json
{
  "Action": [
    "ec2:RunInstances",
    "ec2:DescribeInstances",
    "ec2:DescribeInstanceTypes",
    "servicequotas:RequestServiceQuotaIncrease"
  ],
  "Effect": "Allow",
  "Resource": "*"
}
```

### Need Help?

Open an issue in this repository or contact your AWS administrator for assistance.

## Continue to deploying the [pipeline and infrastructure][up-next-link]

<!-- Link Groups -->

[docs-docker-download-link]: https://docs.docker.com/desktop/
[docs-nodejs-download-link]: https://nodejs.org/en/download
[docs-aws-cli-download-link]: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
[docs-aws-profile-setup-link]: https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html
[docs-aws-sam-cli-download-link]: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html
[up-next-link]: https://github.com/arrat-tools/deploy/blob/main/guide/01-deploy-the-infrastructure.md
