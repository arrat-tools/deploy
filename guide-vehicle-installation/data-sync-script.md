<div align="center"><a name="readme-top"></a></div>

<h1 align="center">Data Sync Script</h1>

The road audit data acquisition GUI software comes with a script that allows the user to upload the collected data to the cloud. By default the script is located at:

`<ros_workspace>/src/ra-daq-gui/scripts/data_sync.sh`

> \[!NOTE]
>
> These files should be downloaded when following the vehicle installation guide. You can get started with that guide [here][vehicle-installation-guide-link] before starting the data sync.

## Prerequisites

### AWS CLI

> \[!TIP]
>
> Learn the most up to date steps to set up the [AWS CLI][docs-aws-cli-download-link] by checking it out.

<b>Install the latest linux AWS CLI by running:</b>

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "/awscliv2.zip" && \
unzip /awscliv2.zip -d / && \
sudo /aws/install
```

_If you want the files downloaded to the root directory remember to run `cd ~` beforehand._

## (Optional) Updating the script

You may have changed the `sync_dir` value within the `config/gui.yaml` during configuration of the GUI software in the the [vehicle installation guide][vehicle-installation-guide-link].

If so, update the `sync_dir` variable in this script to match this value.

## Running the script

<b>Run the sync script by running:</b>

```bash
AWS_ACCESS_KEY_ID="<your access key id>" AWS_SECRET_ACCESS_KEY="<your secret access key>" bash ./data-sync.sh "s3://tac-image-staging/"
```

_You may need to update `s3://tac-image-staging/` to the `SessionInputBucketName` generated while deploying the Pipeline and Step Functions during the [infrastructure deployment][infrastructure-deployment-link]. Remember to put `s3://` before and `/` after the SessionInputBucketName_

> \[!NOTE]
>
> You can grab `your access key id` and `secret access key` from the `/arratoperator/credentials/ArratOperator` secret. `your access key id = ACCESS_KEY` and `your secret access key = SECRET_KEY` from the stored secrets's SecretString. These values were generated while deploying the Pipeline and Step Functions during the [infrastructure deployment][infrastructure-deployment-link].
> 
> Navigate to the AWS Secrets Manager through the web portal or run `aws secretsmanager get-secret-value --secret-id /arratoperator/credentials/ArratOperator --profile arrat-cli` to get the values.
>
> _If needed, update arrat-cli to the profile configured during the prerequisites step_

[![][back-to-top]](#readme-top)

<!-- Link Groups -->

[back-to-top]: https://img.shields.io/badge/-Back_to_top-151515?style=flat-square
[docs-aws-cli-download-link]: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
[vehicle-installation-guide-link]: https://github.com/arrat-tools/deploy/blob/main/guide-vehicle-installation/Install_Vehicle_Software.md
[infrastructure-deployment-link]: https://github.com/arrat-tools/deploy/blob/main/guide/01-deploy-the-infrastructure.md
