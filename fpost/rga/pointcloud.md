---
layout: fpost
title: "PointCloud 데이터를 활용한 3D Map 구현"
permalink: /fpost/rga/pointcloud/
author: Jisun Hwang
tags:
  - RGA   
  - PointCloud
  - 3D Mapping
  - ROS2
  - Octomap
  - Velodyne
  - ZED2
  - Jetson ORIN
---

## • 프로젝트 개요
- **목적**:
  - Velodyne 및 ZED2 카메라로부터 PointCloud 데이터를 수집하여 Octomap 라이브러리를 활용한 고품질 3D Map 구현.
  - Depth Estimation 데이터를 활용한 PointCloud 기반 3D Map 생성을 탐구하기 위한 선행 실험 진행.
- **성과**:
  - Velodyne PointCloud 데이터를 필터링하여 실내 구조를 명확히 표현한 3D Map 생성.
  - ZED2 카메라의 Odometry 정보를 활용한 정확한 위치 기반 3D Map 구현.
  - ZED2 카메라의 한계점을 확인하고 ORBSLAM3와 PointCloud 데이터를 접목한 보정 방안 탐색.

---

<figure>
  <div style="text-align:center">
    <img src="/fpost/rga/pointcloud_3d_mapping/img1.png" alt="3D Mapping System Overview" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 1. Velodyne 및 ZED2 기반 PointCloud 데이터를 활용한 3D Map</figcaption>
</figure>

---

### 1. 주요 기능 및 기술 구현

#### 1.1 Docker 환경 구성
- **Ubuntu 22.04 및 ROS2 Humble 기반 컨테이너 환경 구축**:
  - ROS2 Humble, Octomap 라이브러리, Velodyne 및 ZED SDK 설치.
  - Jetson ORIN의 GPU를 활용한 가속화 설정 및 컨테이너 네트워크 통신 구성.

#### 1.2 3D Map 생성 및 필터링
- **Velodyne PointCloud2 데이터**:
  - 불필요한 데이터를 필터링하여 실내 구조를 명확히 표현.
  - Octomap을 활용해 고품질 3D Map 생성.
- **ZED2 카메라 PointCloud2 데이터**:
  - 데이터를 필터링하고 Octomap으로 지도 생성.
  - Velodyne 기반 지도보다 발산 포인트가 많아 품질 한계를 확인.
- **Odometry 정보 활용**:
  - ZED2 카메라의 Odometry 데이터를 이용해 위치 기반 3D Map 생성.
  - 중복 데이터 쌓임 문제를 해결하여 지도 품질 개선.

#### 1.3 Depth Estimation 가능성 탐구
- **선행 실험**:
  - Depth Estimation 데이터를 활용해 PointCloud와 위치 정보를 결합하여 3D Map 생성 가능성 탐구.
  - Velodyne 및 ZED2 데이터를 사용한 대체 실험 수행.

---

### 2. 결과 및 주요 성과

#### 2.1 Velodyne 기반 3D Map
- **성과**:
  - 필터링 후 실내 구조를 명확히 표현한 고품질 3D Map 생성.
- **문제 해결**:
  - 중복 데이터 쌓임 문제를 ZED2 카메라의 Odometry 데이터를 활용해 해결.
  - ZED2 카메라의 IMU 데이터 발산으로 Odometry 정보 부정확 시 지도 품질 저하 확인.

#### 2.2 ZED2 카메라 기반 3D Map
- **성과**:
  - PointCloud 데이터를 활용한 지도 생성 성공.
- **한계**:
  - 데이터 품질이 균일하지 않아 Velodyne보다 낮은 지도 품질 확인.
  - Odometry 데이터 발산 시 정확한 Map 생성이 어려움.

---

### 3. 평가 및 경험

- **SLAM 시스템 설계 및 실험 경험**:
  - Velodyne 및 ZED2 카메라 데이터를 활용한 다양한 3D Mapping 실험 수행.
  - Depth Estimation 데이터와 SLAM 적용 가능성에 대한 이해도 향상.
- **데이터 품질 분석 및 필터링**:
  - PointCloud 데이터를 필터링하여 지도 품질을 향상시키는 알고리즘 설계.
- **개선 방향 탐구**:
  - Odometry 데이터의 한계점을 극복하기 위한 ORBSLAM3와 PointCloud 데이터 결합 아이디어 도출.

---

### 4. 기술 스택

- **OS**: Ubuntu 22.04  
- **SLAM Framework**: Octomap, ORBSLAM3  
- **Sensor**: Velodyne LiDAR, ZED2 Camera  
- **Docker**  
- **ROS2**: Humble  
- **Hardware**: Jetson ORIN  

---

### 5. 결론
PointCloud 데이터를 활용한 3D Mapping 프로젝트는 Velodyne 및 ZED2 카메라 데이터를 이용한 다양한 실험을 통해 3D Map 생성의 가능성과 한계를 분석했습니다. 이를 통해 SLAM 성능 개선 방향을 제안하였으며, 특히 Odometry 데이터의 한계점을 극복하기 위한 새로운 접근법으로 ORBSLAM3와의 데이터 결합 아이디어를 도출하였습니다. 이러한 결과는 대규모 환경에서의 정밀한 지도 생성 및 데이터 처리의 기반이 될 것입니다.
