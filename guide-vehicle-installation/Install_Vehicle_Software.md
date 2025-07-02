## Overview

* What is RA DAQ GUI software
* What is its purpose
* What are the components and their functions

RA-DAQ-GUI is a companion software to the ARRAT (road audit tool) designed to run in the vehicle compute platform that performs the data collection tasks for road audit. It is created as a ROS package and assumes the sensors required for road audit come with ROS packages as well. The two parts of the RA-DAQ-GUI software are:

* Calibration GUI
* Data Acquisition GUI
* Data Sync Script

Below are the sections on:
* Installation
* Configuration
* Calibration Process
* Data Collection Process

## Installation

Here's a step-by-step guide to create a ROS workspace, clone a ROS package, build it with ```catkin_make```, source the environment, and launch a ROS package. The instructions are tailored for Ubuntu (typically used with ROS) and assume ROS Noetic (which uses Python 3 and is supported on Ubuntu 20.04).

✅ Prerequisites

Ensure you have:

* Ubuntu 20.04
* ROS Noetic installed (ROS Noetic install instructions)
* ```catkin tools``` available (```catkin_make``` is used in this guide)

<br>

### 🔧 Step 1: Create a Catkin Workspace

```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```

This will generate the workspace structure:

```css
catkin_ws/
├── build/
├── devel/
└── src/
```


### 🧬 Step 2: Source the Setup File

You need to source your workspace’s setup script each time in a new terminal session (or add it to .bashrc):

```source ~/catkin_ws/devel/setup.bash```

To make it persistent across sessions:

```bash
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

### 🔄 Step 3: Clone a ROS Package into src

Navigate to the src directory and clone the Road Audit Data-Collection GUI software repository from GitHub. 

```bash
cd ~/catkin_ws/src
git clone https://github.com/arrat-tools/vehicle/ra-daq-gui.git
```


### 🛠️ Step 4: Build the Workspace Using catkin_make

Go back to the workspace root and compile:

```bash
cd ~/catkin_ws
catkin_make
```

If there are missing dependencies, install them with rosdep:

```bash
cd ~/catkin_ws
rosdep install --from-paths src --ignore-src -r -y
```

Then re-run ```catkin_make```.


### 📡 Step 5: Source the Workspace After Building

You must source the setup.bash again after building:

```source ~/catkin_ws/devel/setup.bash```

If the step above to make sourcing persistent is followed then this does not have to done each time. Opening a terminal automaticaly sources the workspace.

### 🚀 Step 7: Create Shortcuts (aliases)

Add these two lines in the ~/.bashrc file to have simplified aliases for the launch commands. 

```bash
alias launch_ragui='roslaunch ra-daq-gui gui.launch'
alias launch_racal='roslaunch ra-daq-gui cal.launch'
```


### 🚀 Step 8: Launch a ROS Package

The ra-daq-gui come with two launch files, one for operating the GUI and one for calibrating the system. 

Launch **Data Acquisition GUI** using the command:

`roslaunch ra-daq-gui gui.launch`

or the alias:

`launch_ragui`


Launch **Calibration GUI Launch** using the command:

`roslaunch ra-daq-gui cal.launch`

or the alias:

`launch_racal`

## Configuration

The package has the following file structure:

```css
ra-daq-gui/
├── config/
├   ├──gui.yaml
├   ├──topics_to_record.txt
├   ├──inputs.json
├── launch/
├   ├──gui.launch
└── scripts/
```

From sensor driver documentation: 
1. Determine the launch files for the camera and GPS packages.
2. Determine the topic names for camera images, depth maps, and GPS fix 
3. Enter the information in ```gui.yaml``` like the example below.

The example below contains the default values for all the configuration parameters. Note the data directories where the raw and sync data is stored.

The sensor-specific information is for ZED camera and OxTS GPS sensors. ZED camera also provides depth maps.

<br>

### Config file

```yaml
data_dir: 'road_audit_data'
sync_dir: 'road_audit_data/sync'
topics_file_pkgpath: 'config/topics_to_record.txt'
imgdirname: 'images'
depthdirname: 'depths'
gpsfilename: 'gps.txt'
max_bag_size: 3000
cam_age_tol: 2.0
gps_age_tol: 2.0
gps_required: false
cam_required: false
gps_topic: '/gps/fix'
cam_topic: '/zed2/zed_node/left_raw/image_raw_color/compressed'
depth_topic: '/zed2/zed_node/depth/depth_registered'
cam_image_compressed: true
gps_launch_command: 'roslaunch oxford_gps_eth gps.launch'
cam_launch_command: 'roslaunch zed_wrapper zed2.launch'
```


### User Entry Parameters

Below is a set of parameters that the user must specify to configure the DAQ to work with their specific hardware. In the event the user chooses a different sensor set or a different location to store data, the following parameters will need to be modified. 


| Parameter | Description |
| -------- | ------- |
| ```data_dir``` | Raw data directory |
| ```sync_dir``` | Unit data directory to be synced to cloud |
| ```topics_file_pkgpath``` | File containing list of topics to record |
| ```gps_topic``` | GPS topic for GUI to monitor |
| ```cam_topic``` | Camera topic for GUI to monitor |
| ```gps_launch_command``` | GPS package launch command |
| ```cam_launch_command``` | Camera package launch command |


**Important**

If the `sync_dir` is changed, it must also be updated in the `data_sync.sh` script. 

### Topics to Record

The topics to be recorded are listed in a text file whose path relative to the ROS package is defined by the parameter `topics_file_pkgpath`.

```
/gps/fix
/zed2/zed_node/left_raw/image_raw_color/compressed
/zed2/zed_node/depth/depth_registered
```

The configuration file and topics to record in the example above shows the information entered for OxTS GPS/INS sensor and ZED stereo camera used for testing the GUI. This information should be adapted to the specifics of the user's chosen sensors.

## Launch

The RA-DAQ-GUI package contains two main software components, data collection and calibration. Following are the launch commands to test each of them.

| Process | Launch command  | Alias |
| -------- | ------- | ------- |
Data Collection | ```roslaunch ra-daq-gui gui.launch```  | ```launch_ragui```    |
Calibration | ```roslaunch ra-daq-gui calibration.launch``` | ```launch_racal```     |

## Sync Script

The road audit data acquisition GUI software comes with a script that allows the user to upload the collected data to the cloud. By default the script is located at:

`<ros_workspace>/src/ra-daq-gui/scripts/data_sync.sh`

Make sure the `sync_dir` variable in this script is the same as the same as configured in the GUI software above.

See Sync Script guide for more details on how to execute data syncing.

## References

* Calibration guide
* Data collection operation guide
* Sync Script Guide

