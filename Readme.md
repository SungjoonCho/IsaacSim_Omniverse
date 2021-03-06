## IsaacSim projects (Simulator : Omniverse)
  * 개요 및 개발 환경
  * [Publishing rgb, depth image with ROS](https://github.com/SungjoonCho/IsaacSim_Omniverse#user-content-publishing-rgb-depth-image-with-ros)
  * [외부 Object 올리기](https://github.com/SungjoonCho/IsaacSim_Omniverse#user-content-%EC%99%B8%EB%B6%80-object-%EC%98%AC%EB%A6%AC%EA%B8%B0) 
  * [Pose control with ROS](https://github.com/SungjoonCho/IsaacSim_Omniverse#pose-control-with-ros)
  * Omniverse Reference

## 개요 및 개발 환경

### 개요

* IsaacSim + ROS(melodic)
* Scene에 n개 RRGBD 센서 부착 후 RGB, Depth image들을 각자 다른 topic으로 publish

### 개발 환경 구성(running Omniverse Isaac Sim natively)

* [개발 환경](https://docs.omniverse.nvidia.com/app_isaacsim/app_isaacsim/requirements.html)
  * Ubuntu 18.04
  * RTX 2080 Ti 사용 - Cuda 10.2, cuDNN 8.0.3
  * NVIDIA graphics card drivers version 460(Unity는 최소 440, Omniverse는 최소 460)
  * Isaac SDK(2020.2)
  * ROS Melodic
  
* [Launcher 다운로드](https://docs.omniverse.nvidia.com/app_isaacsim/app_isaacsim/setup.html#isaac-sim-on-omniverse-launcher)

### Omniverse 실행 
  
* Omniverse Launcher 아이콘 클릭 - LAUNCH

### 추가 Asset 다운로드(선택)

* Local에 Nucleus 설치 후 nucleus 서버 통해서 asset 다운로드 가능

1. [Nucleus 설치](https://docs.omniverse.nvidia.com/prod_nucleus/prod_nucleus/installation/workstation.html#installing-using-omniverse-launcher)
2. [asset 저장할 디렉토리 생성, asset 다운로드](https://docs.omniverse.nvidia.com/app_isaacsim/app_isaacsim/setup.html#isaac-sim-setup-nucleus-add-assets)
   
   localhost 디렉토리에 바로 생성이 안돼서 User 폴더 내부에 저장함
   
3. [Asset 파일 설명](https://docs.omniverse.nvidia.com/app_isaacsim/app_isaacsim/assets.html)

## Publishing rgb, depth image with ROS 

### ROS publish 제작

  1. Create - Shape 원하는 물체 배치
  2. Create - Camera 원하는 개수만큼 원하는 위치에 배치, Camera Property에서 parameter 수정 가능 
  3. Create - Isaac - ROS - Camera 를 2번에서 추가한 카메라 개수만큼 추가
  4. ROS_Camera - Property의 Raw USD Properties에서 depthEnabled 체크, prim에 add target - publish하고자 하는 camera 선택
  5. depthPubTopic, rgbPubTopic 수정 (센서 토픽들이 중복되지 않도록 주의)
  6. 시뮬레이션 실행
  7. Rviz에서 확인
  
### 결과

<p align="center">
  <img width="800" height="500" src="https://user-images.githubusercontent.com/80872528/130381577-26aa054e-38d8-4d47-86c5-0a66bb0c4351.png">
</p>

<p align="center">
  <img width="800" height="500" src="https://user-images.githubusercontent.com/80872528/130381555-2a767427-9979-43b5-8e59-c16c8d1e604f.png">
</p>
  
## [외부 Object 올리기](https://docs.omniverse.nvidia.com/app_isaacsim/app_isaacsim/ext_omni_isaac_urdf.html)

### 순서

1. 외부에서 URDF 파일 다운로드
2. /.local/share/ov/pkg/isaac_sim-2021.1.1/exts/omni.isaac.urdf/data/urdf/ 에 임의의 새 폴더 만들고 urdf 파일 저장
3. 아래 그림과 같이 [Built In URDF Files] - [custom] - 원하는 urdf 파일 우클릭 - Convert URDF to USD


<p align="center">
  <img width="800" height="200" src="https://user-images.githubusercontent.com/80872528/130394320-fb30de93-226d-49b1-bfc9-4e931bbc3817.png">
</p>


## Pose control with ROS

* Omniverse
1. Create - Isaac - ROS - Teleport 클릭하면 ROS_Teleport 생김
2. Property - Add Target 클릭하여 ROS로 움직이고자 하는 대상 선택
3. 시뮬레이션 실행

* Python script
1. /.local/share/ov/pkg/isaac_sim-2021.1.1/ros_samples/teleport/ros_pose_client.py main 문의 "/Cubes" 부분에 2번에서 선택한 대상의 경로 입력 (ex. "/World/Capsule")
2. np.array 이용하여 원하는 pose 입력
3. 현재 script의 cube_pos_vec의 경우 0~1 사이의 임의의 수 3개가 x y z로 들어감

* Terminal 1
<pre>
$ conda create -n omni python=3.6
$ conda activate omni
$ pip install -r requirements.txt  (게시된 txt 파일 다운로드)
$ cd .local/share/ov/pkg/isaac_sim-2021.1.1
$ python ros_samples/teleport/ros_pose_client.py
</pre>


##  Omniverse Reference


* [Omniverse Overview](https://docs.omniverse.nvidia.com/app_isaacsim/app_isaacsim/overview.html)
* [Isaac Ros Bridge](https://docs.omniverse.nvidia.com/app_isaacsim/app_isaacsim/ext_omni_isaac_ros_bridge.html)
* [Ros Bridge Commands](https://docs.omniverse.nvidia.com/py/isaacsim/source/extensions/omni.isaac.ros_bridge_ui/docs/index.html#module-omni.isaac.ros_bridge_ui.scripts.commands)
