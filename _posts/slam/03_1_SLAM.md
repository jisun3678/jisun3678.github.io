---
layout: post
image: /assets/images/blog/post-5.jpg
title: "SLAM 3-1강 (Point Cloud Registration & ICP algorithm) 요약"
categories:
    - SLAM
tags:
    - SLAM
toc: true
toc_sticky: true
comments: true
---

Cyrill 교수님의 SLAM 강의를 듣고 정리한 내용을 공유합니다!

## 0. Today's Goal
- Point Cloud Registration이란?  
- Direct Optimal Solution with Known Data Association  
- Why solution used SVD is good?  

---

## 1. 강의 및 자료 소개  

다음 강의와 자료를 기반으로 내용을 정리했습니다:  
- [ICP & Point Cloud Registration - Part 1: Known Data Association & SVD (Cyrill Stachniss, 2021)](https://youtu.be/dhzLQfDBx2Q)  
- [SLAM DUNK Season 2 - Iterative Closest Points](https://youtu.be/BiQx5ISVdxU)  
- Cyrill Stachniss의 [강의 자료 PDF](https://drive.google.com/file/d/13NswuU_xD-OLTMOC3gLc2jpQvjXGS-HD/view?usp=sharing)  

---

## 2. Point Cloud Registration이란?  

Point Cloud Registration은 **두 Point Cloud를 정렬하는 공간 변환(Rotation $R$과 Translation $t$)을 찾는 과정**입니다.  
이는 Mapping 과정에서 Scan matching과 Scan registration을 통해 정확한 주위 환경을 표현하는 데 매우 중요합니다.

### 문제 정의
- **입력**: 두 Point Cloud $\{x_n\}$, $\{y_n\}$와 대응 관계(Correspondence) $C$  
- **목표**: $R$과 $t$를 찾아 두 Point Cloud 간의 유클리디안 거리를 최소화  

식으로 표현하면 다음과 같습니다:  
$$
\{\bar{x_n}\} = R\{x_n\} + t
$$
$$
\text{minimize} \sum_{n} \| y_n - (R x_n + t) \|^2
$$  

---

## 3. Direct Optimal Solution with Known Data Association  

### 개요  
대응 관계가 주어졌을 때, Initial guess 없이 반복(iterate) 과정 없이도 최적의 해를 구할 수 있습니다. 이 방법은 **SVD(Singular Value Decomposition)**을 사용합니다.

### 과정
1. **Translation 계산**  
   - 두 Point Cloud의 질량 중심(center of mass)을 계산  
   $$
   x_0 = \frac{\sum p_n x_n}{\sum p_n}, \quad y_0 = \frac{\sum p_n y_n}{\sum p_n}
   $$  

2. **Cross Covariance Matrix 계산**  
   $$
   H = \sum p_n (x_n - x_0)(y_n - y_0)^T
   $$  

3. **SVD를 이용한 Rotation 계산**  
   - $H = UDV^T$로 분해  
   - $R = UV^T$  

4. **Translation 계산**  
   $$
   t = y_0 - R x_0
   $$  

---

## 4. Why solution used SVD is good?  

### 장점  
1. **Initial guess 불필요**: 초기값 없이도 해를 찾을 수 있음.  
2. **Iterative 과정 없음**: 반복 없이 한 번의 계산으로 결과 도출.  
3. **최적의 해 보장**: $H$가 Full rank일 경우 Unique한 해를 보장.  

### 증명  
1. **Objective Function 정의**  
   $$
   \Phi(R, t) = \sum \|y_n - (R x_n + t)\|^2
   $$
   이를 최소화하는 $R$과 $t$를 찾음.

2. **Translation 업데이트**  
   $$
   t = y_0 - R x_0
   $$  

3. **Rotation 최적화**  
   - $R$을 최적화하는 문제는 아래 식으로 변환:  
     $$
     R^* = \text{argmax}_R \text{tr}(R^T H)
     $$
   - $H$를 SVD로 분해: $H = UDV^T$  
   - 최적의 $R = UV^T$  

---

## 5. 결론  

Known Data Association 상황에서 Point Cloud Registration은 SVD를 활용하여 효율적이고 정확하게 해결할 수 있습니다. 이는 SLAM 및 Odometry 알고리즘의 중요한 기반이 됩니다.  
