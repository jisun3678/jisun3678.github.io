---
layout: fpost
title: "스마트 팩토리 모니터링 시스템"
permalink: /fpost/js_tech/smart_factory/
author: Jisun Hwang
tags: 
  - JS tech  
  - Smart Factory
  - Embedded Systems
  - STM32
  - Bluetooth
  - WiFi
  - Real-Time Monitoring
  - 주식회사영흥
---

## • 프로젝트 개요
- **목적**:
  - 공장에서 실시간 에너지 사용량을 측정 및 분석하여 제품 제작 공정 과정의 효율성을 개선하는 모니터링 시스템 구현.
- **특징**:
  - 실시간 대량 데이터 전송을 지원하는 WiFi 기반 통신.
  - 사용자 친화적인 블루투스 제어 기능.

---

<figure>
  <div style="text-align:center">
    <img src="/fpost/js_tech/img/smart_factory/fig1.png" alt="Smart Factory Monitoring System Overview" style="width:80%;">
  </div>
  <figcaption style="text-align:center">Fig 1. 스마트 팩토리 모니터링 시스템 개요</figcaption>
</figure>

---

### 1. 주요 기능 및 기술 구현

#### 1.1 통신 부문
- **UART**: 계량기와의 데이터 통신을 위한 내부 프로토콜 설계 및 드라이버 제작.  
- **Bluetooth**:
  - 시스템 설정, 시작 및 종료 제어 기능 구현.  
  - 사용자 편의성을 고려한 인터페이스 설계.  
- **WiFi**:
  - 서버와의 통신을 위한 내부 프로토콜 설계.  
  - WiFi 모뎀 펌웨어 설계 및 구현.  

---

### 2. 주요 성과 및 기여

#### 2.1 WiFi 모뎀 펌웨어 100% 개발
- 실시간 대량 데이터 전송을 지원하는 안정적인 통신 시스템 구축.  
- 서버와의 통신 안정성을 확보하여 데이터 관리 효율성을 증대.  

#### 2.2 사용자 경험 개선
- Bluetooth 제어를 통해 간단한 설정 및 시작/종료 제어 기능을 제공하여 사용자 편의성을 향상.  

#### 2.3 데이터 전송 시스템 개선
- 기존 계량기와 달리 대량 데이터를 안정적으로 전송할 수 있는 환경 조성.  

---

### 3. 평가 및 경험

- **통신 프로토콜 설계 및 구현**:
  - WiFi, Bluetooth, UART를 활용한 통합 통신 시스템 설계 및 구현 경험 축적.  
- **사용자 중심 설계**:
  - Bluetooth 기반 사용자 인터페이스 설계를 통해 사용 편의성 증대.  
- **실시간 데이터 처리**:
  - 실시간 데이터 전송 시스템 구축으로 생산 공정 분석 및 효율화 지원.  

---

### 4. 기술 스택
- **MCU**: STM32  
- **통신**: UART, Bluetooth, WiFi  
- **프로토콜**: 내부 통신 프로토콜 설계 및 구현  

---

### 5. 결론
스마트 팩토리 모니터링 시스템 프로젝트는 실시간 데이터를 활용하여 생산 공정의 효율성을 높이고 사용자 중심의 제어 기능을 구현하였습니다. WiFi와 Bluetooth를 통합한 통신 시스템을 통해 안정적인 데이터 전송 환경을 구축하며, 산업 현장에서 요구되는 실시간 모니터링 기술을 성공적으로 구현하였습니다. 이를 통해 통신 프로토콜 설계 및 사용자 중심 기술 구현 경험을 축적하였으며, 향후 스마트 팩토리 솔루션 개발의 기반을 마련하였습니다.
