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

## Running the script

Make sure the `sync_dir` variable in this script is the same as the same as configured in the GUI software during the [vehicle installation guide][vehicle-installation-guide-link].

<b>Run the sync script by running:</b>

```bash
AWS_ACCESS_KEY_ID="<your access key id>" AWS_SECRET_ACCESS_KEY="<your secret access key>" ./data-sync.sh
```

_You will need to grab `your access key id` and `secret access key` for your AWS Account before running the script.  These values are generated when executing the [infrastructure deployment][infrastructure-deployment-link] and are stored in AWS Secrets Manager.  The s3location value in the script is the S3 session input bucket created when the arrat-step-functions CloudFormation template is created during the [infrastructure deployment][infrastructure-deployment-link].  This value will be output by the CLI on successful template deployment and will be displayed in the command line as the SessionInputBucketName.  This value can also be obtained after pipeline creation by navigating to the CloudFormation console in AWS and selecting the arrat-step-functions stack.  Choose the Outputs tab and the required bucket name will be the value displayed with the SessionInputBucketName key._

[![][back-to-top]](#readme-top)

<!-- Link Groups -->

[back-to-top]: https://img.shields.io/badge/-Back_to_top-151515?style=flat-square
[docs-aws-cli-download-link]: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
[vehicle-installation-guide-link]: https://github.com/arrat-tools/deploy/blob/main/guide-vehicle-installation/Install_Vehicle_Software.md
[infrastructure-deployment-link]: https://github.com/arrat-tools/deploy/blob/main/guide/01-deploy-the-infrastructure.md
