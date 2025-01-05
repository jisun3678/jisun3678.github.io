---
layout: fpost
title: "ORBSLAM3과 RTAB-Map을 활용한 SLAM 시스템 구현"
permalink: /fpost/rga/orbslam/
author: Jisun Hwang
tags:
  - RGA   
  - SLAM
  - ROS2
  - ORBSLAM3
  - RTAB-Map
  - Docker
  - Jetson ORIN
---

## • 프로젝트 개요
- **목적**:
  - ROS2(Foxy) 환경에서 ZED2 카메라를 활용한 실내 및 대규모 환경의 SLAM 실험.
  - ORBSLAM3과 RTAB-Map을 활용해 SLAM 성능 비교 및 최적화 수행.
  - Docker를 활용하여 Ubuntu 20.04 기반 컨테이너 환경에서 ROS2 및 SLAM 프레임워크 실행.
  - ORIN 플랫폼에서 GPU 가속을 통한 SLAM 성능 최적화.
- **성과**:
  - Docker 기반 표준화된 실험 환경 구성.
  - ORIN 플랫폼의 GPU 가속을 활용해 실시간 SLAM 처리 성능 개선.
  - ORBSLAM3과 RTAB-Map 성능 비교 및 개선 방안 도출.

---

<figure>
  <div style="text-align:center">
    <img src="/fpost/rga/slam_system_implementation/img1.png" alt="SLAM System Implementation" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 1. ORBSLAM3과 RTAB-Map 성능 비교 실험 개요</figcaption>
</figure>

---

### 1. 주요 기능 및 기술 구현

#### 1.1 Docker 환경 구성
- **Ubuntu 20.04 기반 컨테이너 환경 구축**:
  - Docker를 활용해 Ubuntu 20.04, ROS2(Foxy), ZED SDK, ORBSLAM3, RTAB-Map 등 필요한 패키지 설치.
  - ROS2 토픽 및 메시지 송수신을 위한 컨테이너 간 네트워크 통신 설정.
- **실험 환경 관리**:
  - 컨테이너를 통해 SLAM 실험의 재현성 확보.
  - 동일 환경에서 ORBSLAM3과 RTAB-Map 성능 비교 실험 수행.

#### 1.2 ORBSLAM3 시스템 구현
- **ROS2 및 ZED2 카메라 연동**:
  - 카메라 해상도와 내부 파라미터 최적화.
  - Map Data 저장 기능 활성화 및 Map Viewer 파라미터 수정으로 데이터 확인 용이성 확보.
- **ORB 파라미터 최적화**:
  - Feature 수를 조정해 정확도와 실시간성 간의 균형 확보.
  - 안정적인 Loop Closing을 위한 파라미터 최적화.

#### 1.3 RTAB-Map 시스템 구현
- **3D Mapping 실험**:
  - 실내 환경에서 고품질의 3D Map 생성 성공.
  - 층 변화 시 Loop Closing 기능의 정확도 저하를 관찰.

---

### 2. 실험 및 결과

#### 2.1 ORIN 기반 Docker 환경에서의 실행
- **환경 구성 성과**:
  - Ubuntu 20.04 기반 Docker 컨테이너에서 ROS2(Foxy), ORBSLAM3, RTAB-Map 실행.
  - NVIDIA Docker를 활용한 GPU 가속으로 SLAM 처리 성능 최적화.
- **결과**:
  - 동일한 실험 환경에서 ORBSLAM3과 RTAB-Map의 성능 비교 및 데이터 수집.

#### 2.2 SLAM 비교 결과
- **RTAB-Map**:
  - 실내 1층에서 고품질의 3D Map 생성.
  - 층 변경 시 Loop Closing 기능 실패로 지도 품질 저하.
- **ORBSLAM3**:
  - 층 변화에도 궤적 추적 성능 우수.
  - 대규모 환경(아파트 단지)에서 안정적인 궤적 추적.

---

### 3. 주요 성과 및 기여

- **Docker 및 Ubuntu 20.04 활용**:
  - Docker 컨테이너로 SLAM 시스템 실행 환경 표준화.
  - 안정적이고 재현성 높은 실험 환경 구성.
- **GPU 가속 및 ORIN 활용**:
  - NVIDIA Docker와 Jetson ORIN을 활용한 실시간 데이터 처리 및 대규모 지도 생성 성능 최적화.
- **SLAM 비교 분석 및 개선**:
  - ORBSLAM3과 RTAB-Map의 장단점 분석.
  - Relocalization과 Local Map Tracking 구조 개선 방향 제안.

---

### 4. 기술 스택

- **ROS2**: Foxy  
- **SLAM Framework**: ORBSLAM3, RTAB-Map  
- **Hardware**: ZED2 Camera, Jetson ORIN  
- **Docker**  
- **OS**: Ubuntu 20.04  
- **환경**: 실내 공간 및 대규모 아파트 단지  

---

### 5. 결론
이 프로젝트는 Docker와 ORIN 플랫폼을 활용한 SLAM 환경 표준화와 성능 최적화를 목표로 진행되었습니다. ORBSLAM3과 RTAB-Map의 성능을 체계적으로 비교하고, 각 시스템의 장단점을 파악하여 SLAM 기술 개선에 기여했습니다. 이러한 성과는 대규모 환경에서의 실시간 지도 생성 및 추적 기술의 발전에 중요한 역할을 할 것입니다.
