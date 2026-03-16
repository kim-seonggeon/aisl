# AISL의 여정

[![KR](https://img.shields.io/badge/README-한국어-blue)](./README.ko.md)
[![EN](https://img.shields.io/badge/README-English-red)](./README.md)

<img src="https://capsule-render.vercel.app/api?type=waving&color=413fd9&height=150&section=header&text=내가%20가고%20싶은%20회사에%20취직하는%20날까지!&fontSize=32" />

## 🧠 AISL 프로젝트에 대해서

### 🎯 주요 목표

### 🧰 도구

### 🛠 기술 스택
**Languages**  
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=Python&logoColor=white)

<p><br></p>

---

## 2026년 3월 13일

### 📝 할 일 (2026-03-13)

- [X] 오늘 했던 데이터셋 외에 다른 데이터셋으로 테스트하기
- [X] OpenVINS 정확하게 공부하기

### 📌 메모

- OpenVINS에서 제공하는 데이터셋 중 3가지를 골라서 테스트해봄
  - 테스트할 데이터셋이 rosbag은 다운로드가 되지 않아 rosbag2로 다운로드하여 변환 후 rosbag play를 진행함
- OpenVINS는 이름에서 알 수 있듯이 'Open-Source Visual-Inertial Navigation System'의 약자로, 카메라(Visual)와 관성 측정 장치(IMU, Inertial)를 결합하여 로봇의 위치와 자세를 추정하는 강력한 프레임워크
  - 1. OpenVINS의 핵심: MSCKF 기반의 필터 방식
    - 가장 큰 특징은 MSCKF(Multi-State Constraint Kalman Filter) 알고리즘을 사용한다는 점
      - => MSCKF는 IMU와 Camera 센서를 사용하여 고정된 Feature에 대해서 measurement update(새로운 노이즈 센서 측정과 이전 예측 상태를 결합하여 개선되고 더 정확한 사후 추정치를 생성함)를 수행하여 odometry(휠 엔코더, IMU, 카메라 등 모션 센서 데이터를 사용하여 시작 위치를 기준으로 로봇이나 차량의 상대적인 위치와 자세 변화를 추정하는 기술)를 제공하는 알고리즘
    - ORB-SLAM과의 차이: ORB-SLAM은 주로 '최적화' 기반으로 전체 지도를 그리며 위치를 잡는다면, OpenVINS는 '필터' 기반임
    - 슬라이딩 윈도우: 모든 과거 데이터를 다 들고 있지 않고, 최근의 카메라 프레임 몇 개만 유지하면서 상태를 업데이트함. 그래서 계산량이 적고 실시간성이 매우 뛰어남
      
  - 2. 왜 OpenVINS를 쓸까?
    - 온라인 캘리브레이션(Online Calibration): 카메라와 IMU 사이의 상대적인 위치(Extrinsics)나 시간 차이(Time Offset)를 로봇이 움직이는 동안 실시간으로 스스로 보정함. 수동으로 값을 맞추는 수고를 덜어줌
    - 확장성: 모듈형 구조라 새로운 센서를 추가하거나 알고리즘 일부를 교체하기가 매우 쉬움
    - 정확도와 속도: EKF(Extended Kalman Filter)기반임에도 불구하고 최적화 기반 알고리즘에 뒤처지지 않는 높은 정밀도를 보여줌. 특히 자원이 제한된 드론이나 소형 로봇에서 강력함
      
  - 3. OpenVINS의 구조
    - Feature Tracking: 카메라 이미지에서 앞서 배운 FAST 같은 코너를 찾아 추적함
    - IMU Preintegration: IMU의 가속도/자이로 데이터를 쌓아서 로봇의 대략적인 움직임을 예측함
    - State Update: 카메라 정보와 IMU 예측치를 합쳐서 로봇의 정확한 위치(x, y, z)와 자세(q)를 확정함

### ✅ 결론

<p><br></p>

---

## 2026년 3월 12일

### 📝 할 일 (2026-03-12)

### 📌 메모

<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/OpenVINS(KITTI).png" width="250"/>
<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/OpenVINS(EuRoC).png" width="250"/>

### ✅ 결론

<p><br></p>

---

## 2026년 3월 11일

### 📝 할 일 (2026-03-11)

### 📌 메모

<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/Trajectory%20Visualization.jpeg" width="250"/>
<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/Estimation%20Accuracy.png" width="250"/>

### ✅ 결론

<p><br></p>

--- 

## 2026년 3월 10일

### 📝 할 일 (2026-03-10)

### 📌 메모

### ✅ 결론

<p><br></p>

---

## 2026년 3월 09일

### 📝 할 일 (2026-03-09)

### 📌 메모

### ✅ 결론

<p><br></p>

---
