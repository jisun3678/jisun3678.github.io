---
layout: post
image: /assets/images/blog/post-5.jpg
title: "SLAM 2강 (Least Squares - An Informal Introduction) 요약"
categories:
    - SLAM
tags:
    - SLAM
toc: true
toc_sticky: true
comments: true
---

## 0. Today's Goal
- Least Squares란?  
- Gauss-Newton Method  
- Least Squares와 Probabilistic State Estimation의 관계  

---

## 1. 강의 및 자료 소개  

다음 강의와 자료를 기반으로 내용을 정리했습니다:  
- [Least Squares - An Informal Introduction (Cyrill Stachniss)](https://youtu.be/r2cyMQ5NB1o)  
- [SLAM DUNK Season 2 - An Informal Introduction to Least Squares](https://youtu.be/mY3G_hjrt7A)  
- Cyrill Stachniss의 [강의 자료 PDF](https://drive.google.com/file/d/10d4lTskz_vZ5Buf4wyKhZiaeehA_YTPh/view?usp=sharing)  

---

## 2. Least Squares란?  

### 정의  
Least Squares는 Graph-based SLAM 시스템의 **backend 최적화 도구**로, 관찰값(Observations)이 파라미터보다 많은 경우, **에러를 최소화**하여 정확한 파라미터를 추정하는 최적화 방법입니다.

> 관찰값과 예측값의 차이를 제곱한 에러를 최소화하는 방식  

예를 들어, 4개의 파라미터를 추정하기 위해 5개의 관찰값이 있을 때, 노이즈를 고려해 파라미터를 추정합니다.

### 핵심 개념  
- **에러 함수**: 관찰값 $z_i$와 예측값 $\hat{z_i} = f_i(x)$의 차이로 정의  
  $$ e_i(x) = z_i - f_i(x) $$  

- **목표**: 에러의 제곱합을 최소화하는 $x$ (최적의 상태)를 추정  
  $$ x^* = \text{argmin} \sum_{i=1}^n e_i(x)^T \Omega_i e_i(x) $$  
  여기서 $\Omega_i$는 정보 행렬을 나타냅니다.

---

## 3. Gauss-Newton Method  

Gauss-Newton Method는 **비선형 모델의 최적화 방법**으로, 다음 단계로 구성됩니다:  

### 3-1. Error Function 선형화  
Taylor 급수 전개를 통해 비선형 에러를 선형화:  
$$ e_i(x + \Delta x) \approx e_i(x) + J_i \Delta x $$  
여기서 $J_i$는 Jacobian 행렬입니다.

### 3-2. 편미분 및 최적화  
Global Error를 최소화하기 위해 에러 함수의 편미분을 계산:  
$$ H \Delta x = -g $$  
- $H$: Hessian 행렬  
- $g$: Gradient 벡터  

### 3-3. $\Delta x$ 업데이트  
위 식을 풀어 $\Delta x$를 구하고, 새로운 $x$를 업데이트:  
$$ x \leftarrow x + \Delta x $$  

### 3-4. 반복  
최적의 $x$를 찾을 때까지 위 과정을 반복합니다.

---

## 4. Least Squares와 Probabilistic State Estimation의 관계  

### 관계  
- Least Squares와 Probabilistic State Estimation은 **같은 최적화 문제를 푸는 방법**입니다.  
- Probabilistic State Estimation에서 **Gaussian 가정** 하에 Maximum Likelihood를 추정하면, Least Squares로 에러를 최소화하는 과정과 동일한 결과를 얻습니다.  

---

이 포스팅은 SLAM 시스템뿐만 아니라 다양한 엔지니어링 문제에도 활용 가능한 Least Squares의 핵심 내용을 다룹니다. 이를 잘 이해하면, 비선형 최적화 문제를 효과적으로 해결할 수 있습니다!
