# Handover system

## Hardware setup
This system include two computing units for HANet handover grasping task, "nuc" for robot arm controlling and sensors, "WS" for HANet inference and handover server and client which has gpu device. Another device "VR_WS" is for VR task.
|Device   | Usage  | GPU  | IP                                                                                                         |
|:---------:|:------------------:|:---------------:|:--------------------------------------------------------------------------------------------------------------------:|
|NUC  | Robot and sensor contorl              | No           | 192.168.0.185  |
|WS  | HANet Inference and Handover state machine              | Yes           | 192.168.0.161  |
|VR_WS  | VR helmet control              | Yes           | 192.168.0.181  |

![Teaser](figures/system-diagram.png)

## Clone repo
```
$ git clone --recursive git@github.com:ARG-NCTU/handover-system.git
$ cd handover-system
```
For first time use, please pull the docker  
On workstation
```
$ docker pull argnctu/handover_system:gpu
```
On NUC
```
$ docker pull argnctu/handover_system:nuc
```

## Start Docker
On GPU workstation
```
$ source gpu_run.sh
```
On NUC
```
$ source nuc_run.sh
```

## How to Start
### Make workspace
```
docker $ source catkin_make.sh
```

### Start Procman
On nuc, set procman deputy
```
docker $ source environment.sh nuc
docker $ source set_remote_procman.sh eno1
docker $ bot-procman-deputy
```
On WS
```
docker $ source environment.sh ws
docker $ source set_remote_procman.sh eno1
docker $ source start_project.sh
```
![Teaser](figures/procman.png)
### Camera and ViperX300s
Restart 00_sensor_robot on NUC

### Handover server and client
Restart 01_handover on workstation. We use [Actionlib](http://wiki.ros.org/actionlib) and [Smach](http://wiki.ros.org/smach) with ROS to control our system. First restart "handover_action_server" to initial server of FSM (Finie State Machine), and restart the "handover_xxx_client" according to different tasks. Here are three examples.
<p float="left">
  <img src="figures/multi-view-smach.png" width="250" title="multi-view grasping" />
  <img src="figures/cl-smach.png" width="252" title="close-loop grasping"/> 
  <img src="figures/simple-samch.png" width="305" title="simple grasping"/>
</p>
