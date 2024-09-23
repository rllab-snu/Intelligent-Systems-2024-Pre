# Intelligent Systems 2024
This is the repository for the student projects of the 'Introduction to Intelligent Systems' course at Seoul National University.
rccar_gym environment codes are originated from [F1TENTH Gym](https://github.com/f1tenth/f1tenth_gym) repository.

> Original author of F1TENTH Gym: *Hongrui Zheng*
 
> (Special Thanks to *Hyeokjin Kwon, Geunje Cheon, Junseok Kim* for editing rccar_gym)

> Author of this repo: *Minsoo Kim, Yoseph Park, Subin Shin*

## RCCar Gym Environment Setting
We recommend installing this package inside a virtual environment such as [Anaconda](https://www.anaconda.com) (or virtualenv).

```shell
conda create -n rccar python=3.8
conda activate rccar

git clone https://github.com/rllab-snu/Intelligent-Systems-2024-Pre.git
cd IS2024_ws/rccar_gym
pip install -e .
```
This will install a gym environment for the RCCar and its dependencies.

## ROS2 Setting
We use ROS2 foxy to run gym environment and project codes.

First, install ROS2 foxy by following the [documentation](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html).

To build the ROS2 packages to use our specific python virtual environment, we should install colcon building tools to our python environment.

Assuming the virtual environment is activated, i.e. `conda activate rccar`,

```shell
pip install colcon-common-extensions
```
This enables installed files resulting from colcon build to use desired package in our environment.

Now, install dependencies and build the packages.

```shell
cd IS2024_ws
rosdep update --rosdistro foxy
rosdep install -i --from-path src --rosdistro foxy -y
colcon build --symlink-install
```
Note that `--rosdistro foxy` is required for `rosdep update` since foxy is an end-of-life version.

Note that `--symlink-install` is required to use modified python files directly without building again.

After building the package, we should use following command in every terminal we want to use our packages.

```shell
source install/setup.bash
```

## Running System by ROS2 Commands
To run the node activating rccar gym, use following command in the first terminal.

```shell
ros2 run rccar_bringup rccar_bringup
```
To run the node which enables keyboard control, use following command in the second terminal.

```shell
ros2 run rccar_bringup keyboard_control
```
