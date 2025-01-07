---
layout: post
image: /assets/images/blog/post-5.jpg
title: "SLAM 1강 (Introduction to SLAM) 요약"
categories:
    - SLAM
tags:
    - SLAM
toc: true
toc_sticky: true
comments: true
---

## 0. Today's Goal
- SLAM이란 무엇인가?  
- Offline SLAM vs Online SLAM  
- SLAM이 왜 어려운가?  
- SLAM의 여러 Pipelines  

---

## 1. 강의 및 자료 소개  

다음 강의와 자료를 기반으로 내용을 정리했습니다:  
- [Introduction to SLAM (Cyrill Stachniss, 2020)](https://www.youtube.com/watch?v=0I30M6yTklo)  
- [SLAM DUNK Season 2 - Introduction to SLAM](https://www.youtube.com/watch?v=d1TvU_jvMsE&list=PLubUquiqNQdP_H6uUmU-9f0y_LheA3Hil&index=1)  
- Cyrill Stachniss의 [강의 자료 PDF](https://drive.google.com/file/d/1aUgC8A7LwQleEBmAJMs9l6NyDKMVBwE0/view?usp=sharing)  

주요 강의 내용은 다음과 같습니다:
- **Graph-based SLAM using pose graphs**  
- **Graph-based SLAM with landmarks**  
- **Robust optimization in SLAM**  
- **State estimation using cameras**  

---

## 2. SLAM이란?  

**SLAM (Simultaneous Localization and Mapping)**은 로봇이 이동하며 자기 위치를 추정(Localization)하고 주변 환경의 지도를 작성(Mapping)하는 기술입니다.  
SLAM은 서로 의존적인 Localization과 Mapping을 동시에 수행해야 하므로 "닭이 먼저냐, 달걀이 먼저냐"라는 문제로 비유됩니다.  

### SLAM에서의 어려움  
- 센서 노이즈 (IMU, Laser 등)  
- 데이터 정확성 부족  

### SLAM의 목적  
- Loop closure를 통해 에러를 보정할 수 있음  
- 최소한의 환경 정보로 시작 가능  

---

## 3. Offline SLAM vs Online SLAM  

SLAM 시스템은 크게 Offline SLAM과 Online SLAM으로 나뉩니다.  

1. **Offline SLAM (Full SLAM)**  
   - 모든 센서 데이터를 수집한 뒤, 지도와 경로를 계산  
   - 더 정확한 결과를 얻기 위해 사용  

2. **Online SLAM**  
   - 실시간으로 지도와 현재 위치를 계산  
   - 현재 로봇의 pose만 고려  

수식적으로는 $z_{1:T}$와 $u_{1:T}$를 통해 $x_{1:T}$와 $m$을 확률적으로 추정합니다.  

---

## 4. SLAM이 어려운 이유  

SLAM의 주요 난관은 **불확실성**입니다.  
예를 들어, 로봇이 관찰한 Landmark와 실제 Landmark 간의 오차는 로봇의 Pose에 따라 달라질 수 있습니다.  
이를 해결하기 위해 **Data Association**이 필요합니다.  

---

## 5. SLAM의 여러 Pipelines  

SLAM은 다음 세 가지 주요 접근 방식으로 나뉩니다:
1. **Kalman Filter**  
2. **Particle Filter**  
3. **Graph-based SLAM**  

Graph-based SLAM은 Motion Model과 Observation Model을 활용하며, 아래와 같은 구조로 표현됩니다:

### Motion Model  
- 로봇의 이전 Pose와 관측 값을 기반으로 현재 Pose를 추정  

### Observation Model  
- Landmark의 위치를 추정  

두 모델 모두 Gaussian 또는 Non-Gaussian 확률 분포로 표현될 수 있습니다.

---

본 요약은 주요 개념과 기법을 간단히 정리한 내용으로, 자세한 내용은 강의를 참고하시기 바랍니다!  
