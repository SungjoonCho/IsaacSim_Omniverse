## IsaacSim projects (Simulator : Omniverse)

  * Publishing rgb, depth image with ROS
  * 외부 Object 올리기 
  
## Publishing rgb, depth image with ROS 

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
  
### ROS publish 제작

  1. Create - Shape 원하는 물체 배치
  2. Create - Camera 원하는 개수만큼 원하는 위치에 배치, Camera Property에서 parameter 수정 가능 
  3. Create - Isaac - ROS - Camera 를 2번에서 추가한 카메라 개수만큼 추가
  4. ROS_Camera - Property의 Raw USD Properties에서 depthEnabled 체크
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
  
## 외부 Object 올리기

### 순서

1. 외부에서 URDF 파일 다운로드
2. /.local/share/ov/pkg/isaac_sim-2021.1.1/exts/omni.isaac.urdf/data/urdf/ 에 임의의 새 폴더 만들고 urdf 파일 저장
3. 아래 그림과 같이 [Built In URDF Files] - [custom] - 원하는 urdf 파일 우클릭 - Convert URDF to USD


<p align="center">
  <img width="800" height="200" src="https://user-images.githubusercontent.com/80872528/130394320-fb30de93-226d-49b1-bfc9-4e931bbc3817.png">
</p>
