---
layout: fpost
title: "전기차 충전 시스템 개발 - 과금형 콘센트 및 완속 충전기"
permalink: /fpost/js_tech/ev_charging/
author: Jisun Hwang
tags:
  - JS tech   
  - EV Charging
  - Embedded Systems
  - STM32
  - OCPP 1.6
  - FreeRTOS
  - RFID
---

## • 프로젝트 개요
- **목적**:
  - **과금형 콘센트**: 기존 주차장의 220V 콘센트를 활용하여 간편하게 설치 가능한 충전 솔루션 제공. NFC 기반 사용자 인증으로 도전 방지 및 충전 기록 관리.
  - **완속 충전기**: 7kWh 및 11kWh 모델 개발, SAE J1772 규격 충족을 통한 안정적 충전 제공.
  - **추가 요구사항**: 고객사 요청에 따라 MCU 변경 및 기능 최적화, 인증 진행.
- **적용 사례**:
  - 고객사 납품 완료 후 현장 설치 및 운영 지원.

---

<figure>
  <div style="text-align:center">
    <img src="/fpost/js_tech/img/ev_charging/fig1.png" alt="EV Charging System Overview" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 1. 전기차 충전 시스템 개요</figcaption>
</figure>


<figure>
  <div style="text-align:center">
    <img src="/fpost/js_tech/img/ev_charging/fig2.png" alt="EV Charging System Overview" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 2. 전기차 충전 시스템 개요</figcaption>
</figure>


<figure>
  <div style="text-align:center">
    <img src="/fpost/js_tech/img/ev_charging/fig3.png" alt="EV Charging System Overview" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 3. 전기차 충전 시스템 개요</figcaption>
</figure>


<figure>
  <div style="text-align:center">
    <img src="/fpost/js_tech/img/ev_charging/fig4.png" alt="EV Charging System Overview" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 4. 전기차 충전 시스템 개요</figcaption>
</figure>

---




### 1. 개발 및 변경 이력

#### 1.1 AT32 기반 초기 개발
- **기능 구현**:
  - **통신**:
    - NFC 및 계측부 통신 드라이버 제작(UART 1, UART 2).  
    - WiFi 통신 드라이버(AP 모드, 링버퍼 기반 구현).  
    - WIZnet Ethernet 컨트롤러를 활용한 TCP/IP Server & Client 구현.  
  - **제어 및 디스플레이**:
    - Relay를 통한 사용자 승인 후 전압 공급 제어.  
    - LED Display 동작 드라이버 제작.  
  - **Pilot**:
    - SAE J1772 규격에 따른 충전 드라이버 설계(ADC 기반 전압 감지, PWM 통신).  
  - **운영체제**:
    - Bare Metal 및 FreeRTOS 병행 개발, FreeRTOS 포팅 완료.  
- **성과 및 평가**:
  - TCP/IP 통신과 FreeRTOS 기반 멀티태스킹 환경 구현.  
  - 형식 승인용 펌웨어 구현 완료.  

#### 1.2 Arduino(ESP32) 변경
- **기능 구현**:
  - **통신**:
    - OCPP 1.6(core) 및 고객사 자체 프로토콜 적용.  
    - 자체 RFID 모듈과 MCU 간 내부 프로토콜 설계(UART 2).  
    - Ethernet 통신 드라이버 구현(SPI).  
  - **제어 및 디스플레이**:
    - Relay 및 LED Display 제어 드라이버 제작.  
- **성과 및 평가**:
  - 형식 승인 및 KC 인증, OCPP 1.6 인증 완료.  
  - 고객사 요구사항 대응 및 프로젝트 관리 역량 강화.  

#### 1.3 STM32 기반 변경 및 기능 확장
- **기능 구현**:
  - **통신**:
    - 기존 ESP32 소스를 STM32 HAL 및 STM32duino로 포팅.  
    - PLC 통신 기반 PnC 기능 구현 준비.  
  - **제어 및 디스플레이**:
    - PWM DMA를 활용한 RGB LED 제어 드라이버 제작.  
    - Relay를 통한 전압 공급 제어.  
  - **Pilot**:
    - SAE J1772 규격 충족을 위한 충전 드라이버 개선.  
    - ADC 및 PWM 기반 상태 판단 알고리즘 구현.  
- **성과 및 평가**:
  - RGB LED 제어에서 PWM DMA 활용으로 다양한 색상 구현.  
  - SAE J1772 및 KC 61851 규격 이해도 증대.  

#### 1.4 RFID 모듈 개발
- **기능 구현**:
  - SPI 기반 RFID 드라이버 개발 및 태그 지원(ISO-14443 TYPE-A, Mifare, T-Money, Cashbee).  
- **성과 및 평가**:
  - 데이터 시트와 실제 동작 불일치 문제를 실험 데이터를 통해 해결.  
  - 고객사 요구사항을 충족하는 RFID 카드 인식 기능 개발.  

---

### 2. 기여도 및 평가

- **MCU 변경 및 소프트웨어 포팅**:  
  - AT32 → Arduino(ESP32) → STM32로 변경하며 각 환경에 맞는 펌웨어 설계 및 포팅 성공.  
- **충전기 판매를 위한 인증 경험**:  
  - 전기용품 안전 인증(KC), 형식 승인, OCPP 1.6 인증 절차를 주도적으로 수행.  
- **기술적 성과**:  
  - TCP/IP, ADC, PWM, SPI, DMA 등 다양한 기술 이해도 향상.  
  - 데이터 시트와 실제 동작 불일치 문제를 실험 데이터를 통해 해결.  
- **제품 상용화**:  
  - 기존 상용 RFID 모듈(단가 약 30000원)을 자체 설계로 단가를 3000원 수준으로 대폭 절감.  
  - 고객사 납품 완료 후 운영 지원 및 요구사항 대응.  

---

### 3. 기술 스택
- **MCU**: AT32, ESP32, STM32  
- **통신**: UART, SPI, Ethernet(TCP/IP), WiFi, NFC, RFID, PLC  
- **저장 및 제어**: EEPROM, PWM DMA, LED, Relay  
- **프로토콜**: OCPP 1.6(core), ISO 15118, SAE J1772  
- **운영체제**: Bare Metal, FreeRTOS  

---

### 4. 결론
전기차 충전 시스템 개발 프로젝트는 다양한 MCU 플랫폼과 프로토콜 환경에서 요구되는 기능을 성공적으로 구현하며, 고객사 요구사항을 충족하는 맞춤형 솔루션을 제공했습니다. 인증 절차를 주도적으로 수행하고, 상용화 단가를 절감하는 등의 성과를 통해 기술적, 상업적 성공을 모두 이뤘습니다. 이 경험은 향후 고도화된 충전 시스템 개발과 글로벌 시장 진출의 기반이 될 것입니다.
