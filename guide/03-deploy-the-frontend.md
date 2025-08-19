<div align="center"><a name="readme-top"></a></div>

<!-- SHIELD GROUP -->
<div align="center">

[![][installation-shield]][installation-link]
[![][license-shield]][license-link]

</div>

<h1 align="center">03. Deploying the Frontend</h1>

**💡 Hint:** We recommend following guides for local development and updates through the original [repository][link-to-repo] to avoid potential misconfiguration.

> \[!NOTE]
>
> If you are unfamiliar with the installation process of the AWS CLI, you can get started with the prerequisites by following the steps [here][back-to-prerequisites]

[![][back-to-top]](#readme-top)

## Fork the repository

To allow AWS to have access to the ARRAT frontend, fork the public [ARRAT repository][link-to-repo]

![Fork the ARRAT frontend](/images/deploy-frontend-fork-repo.png)

## Deploying to AWS

**Getting started**

1. Navigate to Amplify console and press _create new app_

![Create new Amplify Application](/images/frontend-step-create-application.png)

**Choose your git provider**

1. Select your git provider
2. Follow their permissions guide and remember to give permission to access the ARRAT repo

![Select git provider](/images/frontend-step-select-repository.png)
![Follow GitHub setup instructions](/images/frontend-step-github-auth.png)

**Selecting repository and branch**

![Select repository and branch](/images/frontend-step-add-repository-and-branch.png)

**Build settings**

1. Choose application name
2. Add `pnpm build` for build script (if needed)
3. Navigate to _Advanced Settings_
4. Add _Environment Variables_

![Update Amplify build settings](/images/frontend-step-app-settings.png)

```bash
# Standard Open Street Map tile set
NEXT_PUBLIC_TILE_SET_ATTRIBUTION=&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors
NEXT_PUBLIC_TILE_SET_URL=https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png

# Esri Satellite tile set
NEXT_PUBLIC_SATELLITE_TILE_SET_ATTRIBUTION=Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community
NEXT_PUBLIC_SATELLITE_TILE_SET_URL=https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}

SERVER_IMAGES_URL= # Add your `CloudFrontDomain` from `deploying the infrastructure.` This should be prefixed with `https` (e.g., https://<your domain>)
SERVER_IMAGES_REMOTE_PATTERN_PROTOCOL=https # Update to your server protocol
SERVER_IMAGES_REMOTE_PATTERN_HOST_NAME= # Add your `CloudFrontDomain` from `deploying the infrastructure.` This should be prefixed with `https` (e.g., <your domain>)
SERVER_IMAGES_REMOTE_PATTERN_PATHNAME=/**/* # Add your server path name here (e.g., /**/*)

SERVER_SESSION_API_BASE_URL= # Add your `WebEndpoint` API deployment URL from `deploying the api step`.
```

_Read more about Next.js `remote patterns` [here](https://nextjs.org/docs/14/app/api-reference/components/image#remotepatterns)_

**Deploy to Amplify**

Review and confirm that the setup was correct then press the `Save and deploy` button.

### Continuous Deployment

Set up continuous deployment through AWS Amplify Console by connecting your repository.

### Custom Domain Configuration

1. **Add Custom Domain:**
   Follow the steps in the AWS Amplify Console to add a custom domain to your project.
2. **Update DNS Records:**
   Update your DNS provider with the necessary records provided by AWS Amplify.

[![][back-to-top]](#readme-top)

## 6. Troubleshooting and FAQs

### Common Issues

- **Error: Amplify push fails**
  - **Solution:** Ensure that your AWS CLI is properly configured with the correct credentials and region.

<a name="faq"></a>

### FAQs

- **How do I update dependencies?**
  - **Answer:** Run `pnpm update` to update your project dependencies.

### Additional Troubleshooting

- **How do I debug authentication issues?**
  - **Solution:** Check the AWS Amplify documentation and ensure your backend configurations are correct.
- **How do I handle CORS issues?**
  - **Solution:** Configure CORS settings in the AWS Amplify Console and update your API settings accordingly.

For more troubleshooting tips, refer to the AWS Amplify Documentation.

[![][back-to-top]](#readme-top)

<!-- Link Groups -->

[installation-link]: https://github.com/arrat-tools/frontend/blob/main/README.md
[installation-shield]: https://img.shields.io/badge/Docs-blue?style=flat-square&logo=readthedocs&color=3b82f6&labelColor=334155&logoColor=f5f5f5
[license-link]: https://github.com/arrat-tools/frontend/tree/main?tab=MIT-0-1-ov-file
[license-shield]: https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square&color=3b82f6&labelColor=334155
[back-to-top]: https://img.shields.io/badge/-Back_to_top-151515?style=flat-square
[link-to-repo]: https://github.com/arrat-tools/frontend
[back-to-prerequisites]: https://github.com/arrat-tools/deploy/blob/main/guide/00-prerequisites.md
