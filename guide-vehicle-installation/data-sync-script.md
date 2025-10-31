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

_You will need to grab `your access key id` and `secret access key` for you AWS Account before running the script._

[![][back-to-top]](#readme-top)

<!-- Link Groups -->

[back-to-top]: https://img.shields.io/badge/-Back_to_top-151515?style=flat-square
[docs-aws-cli-download-link]: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
[vehicle-installation-guide-link]: https://github.com/arrat-tools/deploy/blob/main/guide-vehicle-installation/Install_Vehicle_Software.md
