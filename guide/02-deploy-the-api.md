<div align="center"><a name="readme-top"></a></div>

<!-- SHIELD GROUP -->
<div align="center">

[![][installation-shield]][installation-link]
[![][license-shield]][license-link]

</div>

<h1 align="center">02. Deploying the API</h1>

**💡 Hint:** We recommend following guides for local development and updates through the original [repository][link-to-repo] to avoid potential misconfiguration.

Our API allows the frontend to interact with and view what's been uploaded and sent through the pipeline deployed in the previous step. It gives access to what units and sessions are currently available to view, update and maintain metadata associated to these sessions, and more.

> \[!NOTE]
>
> If you are unfamiliar with the installation process of the AWS CLI, you can get started with the prerequisites by following the steps [here][back-to-prerequisites]

## Deploying to AWS

_If needed, update `arrat-cli` to the profile configured during the prerequisites step_

<div align="center">

  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="/images/deploy-api-commands.png">
    <img height="240" src="/images/deploy-api-commands.png" alt="Deploy commands for the ARRAT API">
  </picture>

</div>

[![][back-to-top]](#readme-top)

## Continue to deploying the [Frontend][up-next-link]

<!-- Link Groups -->

[installation-link]: https://github.com/arrat-tools/api/blob/main/README.md
[installation-shield]: https://img.shields.io/badge/Docs-blue?style=flat-square&logo=readthedocs&color=3b82f6&labelColor=334155&logoColor=f5f5f5
[license-link]: https://github.com/arrat-tools/api/blob/main/License
[license-shield]: https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square&color=3b82f6&labelColor=334155
[back-to-top]: https://img.shields.io/badge/-Back_to_top-151515?style=flat-square
[link-to-repo]: https://github.com/arrat-tools/api
[up-next-link]: https://github.com/arrat-tools/deploy/blob/main/guide/03-deploy-the-frontend.md
[back-to-prerequisites]: https://github.com/arrat-tools/deploy/blob/main/guide/00-prerequisites.md
