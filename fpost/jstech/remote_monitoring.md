---
layout: fpost
title: "원격 검침 중앙 관제 시스템(민수)"
permalink: /fpost/js_tech/remote_monitoring/
author: Jisun Hwang
tags:   
  - Remote Monitoring
  - Embedded Systems
  - Communication Protocols
  - Energy Management
  - Firmware Development
  - RS485
---

## • 프로젝트 개요
- **목적**: 수도, 온수, 난방, 가스, 냉방, 전기 등의 실시간 에너지 사용량 데이터를 수집하여 서버로 전송, 이를 통해 관리비 과금 및 에너지 사용 분석 리포트를 제공.  
- **적용 사례**: 전국 다수의 집합 건물에 시공되어 원격 검침 서비스로 운영 중.  

---

<figure>
  <div style="text-align:center">
    <img src="/fpost/js_tech/remote_monitoring/img1.png" alt="Remote Monitoring System Overview" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 1. 원격 검침 중앙 관제 시스템 개요</figcaption>
</figure>

---

### 1. 주요 기능 및 기술 구현

#### 1.1 통신 부문
- **UART 1 (RS485)**: 계량기와의 통신을 위한 드라이버 제작.  
- **UART 2 (RS485)**: DCU(또는 서버)와의 통신을 위한 드라이버 제작.  
  - 원격으로 TCU 설정 변경 및 Bypass 기능 구현.  
- **UART 3 (RS485)**: 월패드와의 통신을 위한 드라이버 제작.  
  - 6개 제조사별 프로토콜 적용으로 커스터마이징된 안정적 통신 제공.  
- **UART 4 (DCPLC)**: 설비미터(수도, 온수, 가스 등)와의 통신을 위한 드라이버 제작.  

#### 1.2 저장 부문
- **I2C (EEPROM)**: 사용 환경에 따른 기본값 설정 및 계측 데이터 저장을 위한 드라이버 제작.  

#### 1.3 포트 제어
- **GPIO Input (5개)**: 펄스 신호를 이용한 에너지 사용량 계측.  
  - Timer Interrupt 기반의 유의미한 데이터 판별 알고리즘 구현.  

---

### 2. 주요 성과 및 기술적 기여

#### 2.1 통신 프로토콜
- **다양한 프로토콜 구현**: RS485, DCPLC, I2C 등 다중 프로토콜 이해 및 구현.  
- **월패드 통신 최적화**: 제조사별 맞춤 프로토콜 적용 및 안정적인 데이터 송수신 구축.  

#### 2.2 데이터 신뢰성 강화
- **검증 알고리즘 구현**: 값의 증가분 검증을 통해 비정상적인 데이터를 필터링.  
- **상태 유지 조건 추가**: TCU 교체 시 기존 데이터 복원을 위한 3회 유지 조건 구현.  

#### 2.3 상용화 및 유지보수
- TCU 및 DCU 펌웨어 **100% 개발** 및 양산 납품 완료.  
- 유지보수 과정 참여를 통한 제품 안정성 확보.  

---

### 3. 기술 스택
- **하드웨어**: RS485, DCPLC, I2C, GPIO.  
- **펌웨어**: Timer Interrupt, 알고리즘 설계.  
- **기여도**: TCU 및 DCU 펌웨어 100% 개발 및 유지보수 전담.  

---

<figure>
  <div style="text-align:center">
    <img src="/fpost/js_tech/remote_monitoring/img2.png" alt="System Workflow" style="width:90%;">
  </div>
  <figcaption style="text-align:center">Fig 2. 원격 검침 시스템 통신 및 데이터 흐름</figcaption>
</figure>

---

### 4. 평가 및 경험
- 통신 프로토콜 설계 및 구현 능력 강화.  
- 데이터 신뢰성을 판단하는 알고리즘 설계 및 문제 해결 역량 향상.  
- 제품의 설계, 개발, 양산, 유지보수에 이르는 전체 수명 주기 경험.  

---

### 5. 결론
이 프로젝트를 통해 다양한 통신 프로토콜 구현 및 데이터 신뢰성 강화의 중요성을 체감했으며, 이를 바탕으로 제품의 상용화와 안정성 확보에 기여하였습니다. 이러한 경험은 에너지 관리 시스템과 임베디드 기술이 융합된 실제 환경에서의 솔루션 제공 역량을 한층 더 강화할 수 있는 계기가 되었습니다.  
