# 形智自动驾驶（SonicAutoDrive）软件安装

# 感知网

## cuda_bevfusion BEVFusion目标检测功能包

- 接收点云与图像信息
- 发布map坐标系下目标检测结果

### Getting Started

- 依赖：ROS，python>=3.8，docker
- build: catkin_make
- run: rosrun cuda_bevfusion cudabevfusion_concatlidar_ros_1cam.py

## det_lane 车道线检测功能包

- 接收小车定位信息，图像数据
- 车道线感知 + 深度估计
- 发布车道线
- 实现车道线检测功能

### Getting Started

- 依赖：ROS，python>=3.8
- build: catkin_make
- run: rosrun det_lane det_lane_node.py

## object_tracking 目标跟踪功能包

- 接收感知目标
- 进行目标跟踪

### Getting Started

- 依赖：ROS，python>=3.8
- build: catkin_make
- run: rosrun object_tracking objects_tracking_ab3d_bevfusion.py


# 规划网kxdun_planner

## Description

kxdun_message_change_pkg 定位消息转换包

kxdun_planning_graph 可视化交互包

kxdun_planning_pkg 局部规划包

kxdun_route_pkg 全局规划包

## 编译
catkin_make
如果电脑环境有conda可以用如下命令编译：
catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3

## Run

在确保第一步Apollo容器及其相关功能已经启动，

第一步启动见kxdun_controller

第二步、Ade容器启动及Kxdun系统模块启动

1. 容器加载
   cd /home/apollo/scripts
   ./ade-ros-start.sh
2. 容器进入
   cd /home/apollo/scripts
   ./ade-ros-enter.sh
3. 小车激光雷达模块启动
   cd ~/apollo_drivers
   source ./devel/setup.bash
   roslaunch drivers_pkg drivers_lidar.launch
4. 正前方相机模块启动
   cd ~/penghang/Camera_ZKHY/SmarterEye-SDK-master/wrapper/ros
   source ./devel/setup.bash
   roslaunch zkhy_stereo_d display.launch
5. 小车相机模块启动
   cd ~/apollo_drivers
   source ./devel/setup.bash
   roslaunch camera_driver_pkg camera_driver.launch
   或
   roslaunch drivers_pkg  drivers_camera.launch
6. 定位消息转换模块启动
   cd ~/penghang/KxdunPlanner
   source ./devel/setup.bash
   rosrun kxdun_message_change_pkg message_node
7. 小车全局导航模块启动
   cd ~/penghang/KxdunPlanner
   source ./devel/setup.bash
   roslaunch mission_planner loader_map_and_route.launch
8. 小车局部导航模块启动
   cd ~/penghang/KxdunPlanner
   source ./devel/setup.bash
   rosrun kxdun_planning_pkg kxdun_planning_node

第三步、Cyber_ROS_Bridge 消息转换桥启动

1. 容器加载和进入

cd /home/apollo/adehome/caohong/apollo_ros_bridge_ok
source docker_tools/start_cyber_ros_bridge.sh

2. 更新环境并启动消息转换

source docker_tools/start_env.sh 
./bazel-bin/cyber_ros_bridge/cyber_ros_bridge
注1：步骤三必须满足：第一步中apollo容器已经正常启动；第二步中ade容器中roscore已经正常启动
