---
layout: fpost
title: "스마트 그리드 전기차 충전 시스템"
permalink: /fpost/js_tech/smart_grid/
author: Jisun Hwang
tags:
  - JS tech   
  - Smart Grid
  - Electric Vehicle Charging
  - Embedded Systems
  - PLC Communication
  - STM32
  - Firmware Development
---

## • 프로젝트 개요
- **목적**:
  - Smart Meter를 통해 가정 및 건물의 총 전력 사용량을 모니터링.
  - 누진세 구간 초과 또는 계약 전력 초과를 방지하기 위한 전기차 충전기 제어.
  - 에너지 사용량 리포트를 제공하여 전력 관리의 효율화 달성.
- **특징**:
  - Qualcomm Green PHY Solution 기반 PLC 통신 활용으로 추가 설비 없이 전력선(PLC)을 통해 데이터 송수신 구현.
- **적용 사례**:
  - 도미니카 전기차 판매 업체에 초도 납품 완료.
  - 전기차 구매 고객 가정에 설치 및 운영 중.

---

<figure>
  <div style="text-align:center">
    <img src="/fpost/js_tech/smart_grid_ev_charging/img1.png" alt="Smart Grid EV Charging System Overview" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 1. 스마트 그리드 전기차 충전 시스템 개요</figcaption>
</figure>

---

### 1. 주요 기능 및 기술 구현

#### 1.1 통신 부문
- **UART 1**: 계측부와의 통신을 위한 드라이버 제작.  
- **UART 2 (PLC)**: Qualcomm Green PHY Solution 기반 PLC 통신 드라이버 제작.  
  - 추가 설비 없이 가정 내 전력선을 통해 데이터 송수신.  
- **UART 3**: 디버깅 및 실시간 로그 확인용 드라이버 제작.  

#### 1.2 저장 부문
- **Flash 메모리**:  
  - 설정값 및 데이터를 저장하기 위한 내부 Flash 드라이버 제작.  

#### 1.3 프로토콜
- **내부 프로토콜 설계**:  
  - 전기차 충전기의 계측부-제어부 및 Meter-DCU 간 데이터 통신 프로토콜 설계.  
  - CRC16 기반 데이터 검증 알고리즘 적용.  

---

### 2. 주요 성과 및 기술적 기여

#### 2.1 STM32 기반 펌웨어 개발
- 전기차 충전기 제어부의 펌웨어를 **100% 설계 및 구현**.  

#### 2.2 상용화 및 납품
- 도미니카 전기차 판매 업체에 초도 납품 및 설치 완료.  
- 현지 요구 사항을 반영한 지속적 업데이트 지원.  

#### 2.3 통신 및 데이터 안정성 강화
- PLC 통신 및 CRC16 기반 데이터 검증 알고리즘으로 통신 신뢰도 확보.  
- 모뎀 전원 관리 등 하드웨어 제어 기술을 통해 시스템 효율성 향상.  

---

### 3. 기술 스택
- **MCU**: STM32  
- **통신**: UART, PLC (Qualcomm Green PHY Solution), CRC16  
- **저장**: Flash 메모리  

---

### 4. 평가 및 경험
- **하드웨어 제어 능력 강화**:  
  - 모듈 전원 관리 및 통신 안정성을 위한 하드웨어 제어 기술 습득.  
- **프로토콜 설계 역량 향상**:  
  - PLC 통신 및 CRC16 기반 데이터 검증 알고리즘 설계를 통해 통신 프로토콜에 대한 깊은 이해를 축적.  

---

### 5. 결론
스마트 그리드 전기차 충전 시스템 프로젝트는 PLC 통신과 스마트 에너지 관리를 융합하여 사용자 친화적인 전력 제어 솔루션을 제공하였습니다. 도미니카 시장에서의 성공적인 납품 경험은 글로벌 시장 요구 사항을 충족하는 기술 역량을 입증하였으며, 이러한 프로젝트를 통해 통신 프로토콜 설계와 하드웨어 제어에 대한 기술적 자신감을 확보하였습니다.
