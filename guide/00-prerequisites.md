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

## Continue to deploying the [pipeline and infrastructure][up-next-link]

<!-- Link Groups -->

[docs-docker-download-link]: https://docs.docker.com/desktop/
[docs-nodejs-download-link]: https://nodejs.org/en/download
[docs-aws-cli-download-link]: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
[docs-aws-profile-setup-link]: https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html
[docs-aws-sam-cli-download-link]: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html
[up-next-link]: https://github.com/arrat-tools/deploy/blob/main/guide/01-deploy-the-infrastructure.md
