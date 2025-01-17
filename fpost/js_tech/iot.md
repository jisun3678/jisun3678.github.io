---
layout: fpost
title: "IoT 디지털 3상 전력량계 - 빌딩 에너지 관리 시스템"
permalink: /fpost/js_tech/iot/
author: Jisun Hwang
tags:
  - JS tech   
  - IoT
  - Energy Management
  - STM32
  - MQTT
  - Cat.M1 LTE
  - Embedded Systems
  - SICOMS
---

## • 프로젝트 개요
- **목적**:
  - 한전 고압 계량기의 데이터를 LTE 통신을 통해 서버로 전송.
  - 태양광 발전 전력량 차감 및 잉여 발전량 판매를 위한 송수전 관리.
- **적용 사례**:
  - 광주 지역에서 시연 중, 상용화를 위한 테스트 진행.

---

<figure>
  <div style="text-align:center">
    <img src="/fpost/js_tech/img/iot/fig1.png" alt="IoT 3상 전력량계 개요" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 1. IoT 디지털 3상 전력량계 시스템 개요</figcaption>
</figure>

---

### 1. 주요 기능 및 기술 구현

#### 1.1 통신 부문
- **UART 1**: 계측부와의 통신을 위한 내부 프로토콜 및 드라이버 제작.  
- **UART 2 (Cat.M1 LTE)**:  
  - AT Command를 활용한 LTE 통신 설정.  
  - MQTT 프로토콜과 JSON 포맷을 사용하여 서버 연동 드라이버 제작.  
- **UART 3**: 디버깅 및 실시간 로그 확인을 위한 드라이버 제작.  

#### 1.2 저장 부문
- **I2C (EEPROM)**:  
  - 설정값 및 계측 데이터 저장을 위한 드라이버 제작.  

#### 1.3 디스플레이
- **SPI 기반 LCD 및 터치패드 제어**:  
  - SPI DMA를 사용하여 고속 TFT LCD 모듈 드라이버 포팅.  
  - 터치패드 드라이버 포팅 및 감도 최적화를 위한 오프셋 설정.  

#### 1.4 포트 제어
- **External Interrupt**:  
  - 한전 고압 계량기의 펄스 입력(20,000pulse/kWh)을 전력량으로 변환하는 드라이버 제작.  

---

### 2. 주요 성과 및 기술적 기여

#### 2.1 STM32 기반 펌웨어 100% 개발
- LTE 모듈 기반 안정적인 서버 연동을 구현하여 실시간 데이터 전송 가능.  
- SPI DMA를 활용한 고속 디스플레이 제어로 시스템 성능 향상.  

#### 2.2 하드웨어 개선 기여
- LTE 모듈 전원 관리 회로 추가를 제안하고 설계 반영하여 시스템 안정성 강화.  

#### 2.3 데이터 관리 및 시각화
- MQTT 프로토콜과 JSON 포맷을 통해 데이터를 효율적으로 전송 및 시각화.  
- 터치패드 감도 최적화를 통해 사용자 경험 향상.  

---

### 3. 기술 스택
- **MCU**: STM32  
- **통신**: UART, Cat.M1 LTE, MQTT, JSON  
- **저장**: I2C (EEPROM)  
- **디스플레이**: SPI DMA, TFT LCD, 터치패드  
- **포트 제어**: External Interrupt  

---

### 4. 평가 및 경험

#### 4.1 통신 및 프로토콜 설계
- AT Command, MQTT 프로토콜, JSON 데이터 포맷 설계를 통해 통신 안정성을 확보.  
- ASCII 코드 기반 통신을 활용한 경험 축적.  

#### 4.2 디스플레이 및 하드웨어 제어
- SPI DMA를 통해 TFT LCD와 터치패드 병렬 연결 및 동시 동작 구현.  
- 터치패드 감도 오프셋 설정으로 사용자 경험 최적화.  

#### 4.3 개선 및 과제
- FreeRTOS 도입을 시도했으나 납품 시 적용하지 못했으며, 향후 적용 예정.  
- 터치패드 오프셋 자동 설정 기능 구현 미완으로 추가 개발 필요.  

---

### 5. 결론
IoT 디지털 3상 전력량계 프로젝트는 에너지 관리와 데이터 시각화의 효율성을 높이는 데 중점을 두었습니다. 통신 안정성과 하드웨어 제어 최적화를 통해 시스템 성능을 개선하였으며, 광주 지역에서의 시연을 통해 실사용 환경에서의 안정성을 입증했습니다. 이 프로젝트를 통해 통신 프로토콜 설계, 데이터 처리, 디스플레이 제어 등 다양한 기술적 역량을 강화할 수 있었습니다.
