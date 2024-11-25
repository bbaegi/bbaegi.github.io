---
layout: post
title:  "PX4 Autopilot SITL for ROS2"
date:   2024-11-25 22:05:00 +0900
categories: jekyll update
published: true
---

멀티콥터 시스템 연구개발 업무를 하면서 PX4 SITL을 다룬지 벌써 몇년이 되어가지만, 주로 개발했던 환경은 PX4 1.14 기준으로 ROS1 Melodic 환경이기 때문에, ROS2 Foxy 환경과 연동하는 SITL 환경 구성에 대해 공부도 할 겸 게시글로 작성해보려 한다.

공식 가이드라인을 따라서 진행하며, 기존에 ROS1 시스템에서 진행했던 부분이 적용이 되는지, 추가로 가이드라인에서 손을 대볼 수 있는 요소들이 있을지를 중간중간 시도해볼 예정.

** from docs.px4.io

environment : Ubuntu 20.04

## Download PX4 Source Code

```bash
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
```

```bash
bash ./PX4-Autopilot/Tools/setup/ubuntu.sh
```

reboot.

## First Build

```bash
make px4_sitl gazebo
```

![<launch PX4 gazebo simulation on ubuntu 20.04>](https://prod-files-secure.s3.us-west-2.amazonaws.com/f9410625-7b3d-4775-a0c3-59e9a53286fe/f01ed6e3-7782-4dbf-b190-465bc0603a09/Screenshot_from_2024-10-20_18-57-32.png)

<launch PX4 gazebo simulation on ubuntu 20.04>

## Multi vehicle spawn

libgazebo_ros_init.so error

```bash
sudo apt install ros-foxy-gazebo-ros-pkgs
```

reinstall gazebo / libgazebo

```bash
sudo apt purge gazebo* libgazebo*
```

```bash
sudo apt install gazebo11 libgazebo11-dev ros-foxy-gazebo-ros-pkgs
```

Command

```bash
./Tools/simulation/gazebo-classic/sitl_multiple_run.sh

```

![Screenshot from 2024-10-21 00-28-43.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f9410625-7b3d-4775-a0c3-59e9a53286fe/fec0d022-38d6-4180-8d78-e1bd559cd54a/Screenshot_from_2024-10-21_00-28-43.png)

Option EX)

```bash
./Tools/simulation/gazebo-classic/sitl_multiple_run.sh -m iris -n 4
```

![Screenshot from 2024-10-21 00-29-40.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/f9410625-7b3d-4775-a0c3-59e9a53286fe/b32cf66c-c1c7-4cfe-a7ba-cd89fb6dc9da/Screenshot_from_2024-10-21_00-29-40.png)