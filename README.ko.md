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

## 2026년 3월 16일

### 📝 할 일 (2026-03-13)

- [X] VINS 논문 읽기

### 📌 메모

- OpenVINS의 근원이 VINS의 논문을 찾아서 이 논문을 본격적으로 읽기로 결정
- [VINS-Mono: A Robust and Versatile Monocular Visual-Inertial State Estimator](https://arxiv.org/pdf/1708.03852)
  - 1. VINS-Mono의 핵심 철학: '모든 것을 한 번에 묶어서 푼다(Tightly-Coupled)'
    - : 과거에는 카메라가 계산한 위치 따로, IMU가 예측한 위치 따로 구해서 대충 섞는 방식(Loosely-Coupled)을 썼음. 하지만 VINS-Mono는 카메라가 본 특징점 오차(Vision-Residual)와 IMU가 측정한 가속도/각속도 오차(IMU Residual)를 하나의 거대한 방정식으로 묶어서 동시에 최적화함. 이 방식을 'Tightly-Coupled'라고 부름.
  - 2. 논문의 4단계 파이프라인(흐름도)
    - 1. 측정값 전처리(Measurement Preprocessing)
      - Vision: KLT 알고리즘으로 들어오는 이미지에서 특징점을 추적함
      - IMU Pre-Integration(사전 적분): IMU는 카메라보다 훨씬 빠름. 카메라 프레임 사이사이에 들어오는 수많은 IMU 데이터를 미리 하나로 뭉쳐놓는 기술임. 특히 VINS-Mono는 이때 IMU의 편향(Bias) 오차까지 실시간으로 보정하는 수식을 제안하여 정확도를 끌어올림
    - 2. 초기화(Estimator Initialization)
      - 카메라 한 대(Mono)를 쓰면 실제 거리(Scale)를 알 수 없음
      - VINS-Mono는 정지 상태가 아니라 로봇이 움직이는 와중(on-the-fly)에도 초기화를 성공시키는 강력한 알고리즘을 제안함. 카메라가 대충 그린 뼈대(Vision-Only SfM)와 IMU 데이터를 정렬시켜서 실제 크기(Scale), 중력 방향, 초기 속도, IMU 편향 값을 한 번에 찾아냄
    - 3. 슬라이딩 윈도우 기반 VIO(Local VIO)
      - 최적화 방식은 계산량이 너무 많아진다는 단점이 있음
      - 이를 해결하기 위해 과거의 데이터는 버리고 최근 N개의 핵심 프레임(Key Frame)만 창문(Window)안에 남겨두고 최적화하는 Sliding Window 기법을 사용함
      - 이때 오래된 데이터를 윈도우에서 그냥 삭제하지 않고, Marginalization(주변화)이라는 수학적 기법을 통해 과거 데이터가 품고 있던 정보(Prior)를 압축해서 현재 윈도우에 넘겨줌
    - 4. 4-DOF 글로벌 최적화(Relocalization & Pose Graph Optimization)
      - 아무리 최적화를 잘해도 오래 주행하면 오차가 누적됨
      - DBoW2를 이용해 이미 방문했던 장소를 인식(Loop Detection)하면, 현재 위치를 교정함
      - 가장 멋짐 점은 '4-DOF(x, y, z, yaw)'만 최적화한다는 것임. IMU가 중력을 게속 느끼고 있기 때문에 로봇의 기울어짐(Roll, Pitch)은 이미 절대적으로 정확하게 알고 있으므로, 굳이 계산을 낭비하지 않는 것임
     
### ✅ 결론

- 내 개인 연구 주제에도 연관성이 있는 논문으로 판단되어 계속 읽으면 될듯

<p><br></p>

---

## 2026년 3월 13일

### 📝 할 일 (2026-03-13)

- [X] 오늘 했던 데이터셋 외에 다른 데이터셋으로 테스트하기
- [X] OpenVINS 정확하게 공부하기

### 📌 메모

- OpenVINS에서 제공하는 데이터셋 중 3가지를 골라서 테스트해봄
  - 테스트할 데이터셋이 rosbag은 다운로드가 되지 않아 rosbag2로 다운로드하여 변환 후 rosbag play를 진행함
- OpenVINS는 이름에서 알 수 있듯이 'Open-Source Visual-Inertial Navigation System'의 약자로, 카메라(Visual)와 관성 측정 장치(IMU, Inertial)를 결합하여 로봇의 위치와 자세를 추정하는 플랫폼
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

- OpenVINS 감이 완벽히 잡히지 않아 관련 논문 읽기
- ORB-SLAM 구현해보기

<p><br></p>

---

## 2026년 3월 12일

### 📝 할 일 (2026-03-12)

- [X] OpenVINS 플랫폼 테스트

### 📌 메모

- EuRoC에서 제공하는 데이터셋을 사용했는데 현시점 기준으로는 찾을 수 없어서 갖고 있는 KITTI에서 제공하는 public datasets을 기반으로 테스트하였지만, launch 파일 실행하는 터미널에서 지속적으로 보이는 에러와 실질적으로 rviz 화면에서 아무것도 보이지 않았음
  - 문제점의 원인을 알아보니 subscribe.launch 파일을 실행한 터미널에 뜬 내용을 보면 [Init]: failed static init: platform moving too much 로 KITTI 데이터셋에서 초기 동작으로 인해 정적 초기화 조건이 위반되어 오류가 발생한 것으로 보이고, KITTI의 원본 캘리브레이션 값은 OpenVINS가 사용하는 Kalibr 형식과 다름. 단순히 토픽 이름만 바꾼다고 되는 것이 아니라, KITTI용 가속도/자이로 노이즈 모델과 카메라-IMU 간의 변환 행렬(T)을 직접 계산해서 넣어주지 않으면 필터가 즉시 발산(Divergence)하게 됨
- OpenVINS에서 제공하는 튜토리얼을 샅샅이 살펴보던 중 ros2 기준에 데이터(현시점 기준 ros1은 다운로드 불가, https://docs.openvins.com/gs-datasets.html <- 참고)는 zip파일로 다운로드 할 수 있어 다운 후 ros2 파일을 ros1으로 convert 해줄 수 있는 명령어가 있어 변환하고 테스트했더니 정상적으로 성공
  
<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/OpenVINS(KITTI).png" width="250"/>
<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/OpenVINS(EuRoC).png" width="250"/>

### ✅ 결론

- 오늘 했던 데이터셋 외에 다른 데이터셋으로 테스트하기
- OpenVINS 정확하게 공부하기

<p><br></p>

---

## 2026년 3월 11일

### 📝 할 일 (2026-03-11)

- [X] 공용 데이터셋을 기반으로 SLAM 테스트
- [X] 교수님께 받은 논문 읽기

### 📌 메모

- Visual SLAM 기반으로 돌리게 되면 내가 원하는 건 ORB-SLAM 이지만 설치 때 의존성 문제가 많다고 해서 Visual SLAM 기반으로 돌려본 경험이 있는 랩원에게 OpenVINS 플랫폼를 추천받아 우선 이것부터 SLAM 테스트해보기로 결정(https://github.com/rpng/open_vins <- 참고)
  - 중간중간에 메모리 부족 문제를 여러 번 겪어서 많이 힘들었지만, OpenVINS 시뮬레이션을 성공적으로 구동함
  - 구동 완료 후 나온 두 화면은 OpenVINS가 로봇의 움직임(궤적)을 얼마나 정확하게 추정하고 있는지를 보여주는 성능 지표와 시각화 결과임
  - 첫 번째 이미지: 궤적 시각화(로봇이 움직인 경로를 2D 평면에 그린 것), 두 번째 이미지: 추정 정확도(시뮬레이션이 실시간으로 돌아가면서 "내가 계산한 위치가 실제와 얼마나 차이 나는가?"를 숫자로 보여주는 데이터 창)
  - 교수님께 받은 논문은 멀티 로봇 시스템에서 특징 지도 병합의 정확성과 효율성을 크게 향상시키는 비반복적인 VSLs 기반 기술을 제시하며, 이는 실시간 로봇 시스템 구현에 중요한 기여를 하는 내용

<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/Trajectory%20Visualization.jpeg" width="250"/>
<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/Estimation%20Accuracy.png" width="250"/>

### ✅ 결론

- OpenVINS 프로젝트 후에 이어서 할 내용 진행
- VSLs 기반 기술 논문 계속 읽기

<p><br></p>

--- 

## 2026년 3월 10일

### 📝 할 일 (2026-03-10)

- 교수님과 진지한 면담(개인 연구 주제 선택 관련)
- 연구실 내에 공용 데이터셋을 기반으로 SLAM 테스트

### 📌 메모

- 교수님께서도 내가 생각한 주제들을 좋게 봐주시고 2번째는 다른 랩원이 하고 있어서 1번과 3번을 잘 연관지어서 진행하고 관련 조언을 해주심
  - 1번째 주제에서 '통신 제약' 조건은 통신 분야의 지식이 많이 부족하므로 패스 (혹은 약간의 제약으로 변경)
  - 1번째 주제를 주요 주체로 잡아서 3번째 주제까지 확장, 3번째는 석사 논문으로, 그리고 임무 계획은 AI 사용이 아니면 굳이임
  - Sparse(featrue 포함) Map Merging은 상업 분야에서는 굳이, 국방 분야에서는 필요성이 있고 실용적인 연구로 보임
  - 시험은 알고리즘을 중요시로 해서 시뮬레이션(Matlab 등)부터 시작
  - baseline 잘 잡기
  - ICP+VSLs 조합 잘 해보기
  - 기하학적 정보(랜드마크의 위치 정보) + 클래스 정보
- 공용 데이터셋을 기반으로 SLAM 테스트를 시도했지만, 예상치 못한 문제들에 많이 부딪혀 내일 관련 공부를 했던 랩원에게 도움 요청함

### ✅ 결론

- 교수님께서 보내주시고 추천해주신 논문들 꾸준히 읽고 공부하기
- 내일은 공용 데이터셋 기반의 SLAM 테스트 배우고 확실하게 내 것으로 만들기

<p><br></p>

---

## 2026년 3월 09일

### 📝 할 일 (2026-03-09)

- 정확한 개인 연구 주제를 선택하기 위한 연구

### 📌 메모

- 학부 연구생부터 해오던 멀티로봇 관련 프로젝트를 석사과정 1학년에 받게 되어 이쪽 분야 중에 내용으로 개인 연구를 진행해야겠다고 생각       
- 방산 기업 취업이 최종 목표이므로 내가 원하는 방산 기업에서 원하는 SW R&D 인재상이 무엇인지 어떤 주제를 선택해야 그 기업에 들어가서 다재다능하게 해낼 수 있을지 조사
  - 취업을 우선시 생각해보면 C++/Python 기반 알고리즘 구현 능력, '무인/로봇' 관련 실질적인 프로젝트와 논문(특히 방산 및 자율주행 연관)과 다양한 로봇 플랫폼(지상 4족, UGV, USV 등)에 이식 가능한 실전형 SW 아키텍처 이해가 필요
  - 멀티 로봇 SLAM을 방위나 전장에서 사용하게 되면 고려되는 환경 특성은 GNSS 취약(실내, 지하, 재난/전장, 전자전 환경), 통신 지연 및 두절(분산하고 견고한 SLAM 및 군집 필요), 다수 이기종 로봇(4족 보행, UGV, 드론, USV 등) 혼합과 센서 제한이나 부분적으로 가려지는(연막, 먼지, 어두운 환경, 제한된 FoV LiDAR 등) 내용들이 있음
  - 이걸 기준으로, 방산 기업 로봇/무인 체계에 잘 맞고 논문 및 포트폴리오로도 괜찮은 주제를 3개 정도 압축해 봄
  1. 통신 제약을 고려한 분산 멀티 로봇 SLAM : 중앙 서버 없이(또는 최소 의존) 로봇들이 부분 맵과 포즈를 주고받으며, 통신 끊김이나 지연 상황에서도 점진적으로 글로벌 맵을 일치시키는 분산 혹은 준-분산 SLAM
  2. 제한된 센서 및 시야에서의 강인 멀티 로봇 SLAM : 제한된 FoV LiDAR, 노이즈가 심한 IMU, 카메라 가려짐 등 방산 환경에서 흔한 센서 조약 조건에서 협력적으로 인식 성능을 올리는 멀티 SLAM
  3. 멀티 로봇 SLAM 기반 군집 임무 계획(MUM-T 염두) : 멀티 SLAM 결과(공유 맵, 각 로봇의 불확실도)를 직접 군집 경로 계획, 탐색 그리고 감시 임무 할당에 연결하는 연구
  - 이 중에서 석사 2년 안에 논문과 데모 구현을 한다고 하면, '통신·센서 제약 환경을 고려한 분산 멀티 로봇 SLAM 및 정찰 임무 계획'을 하나의 큰 주제로 잡고, 1년 차에는 SLAM 쪽을, 2년 차에는 임무 계획/군집 쪽을 붙이는 구조가 알맞다고 판단
 
- 간단한 석사 1~2년차 로드맵(연구+취업 준비)
  - 1년차: 기반 다지기 + 1편 수준 결과
    - 0-6개월
      - 이론·코드: ORB-SLAM 계열, pose graph SLAM, LAMP/LAMP2.0 같이 검증된 멀티 로봇 SLAM 시스템 분석 및 구현 연습
      - 언어/도구: C++/Python, ROS2, Git, 기본 PCL/OpenCV/로봇 시뮬레이터(Gazebo/Ignition, Isaac Sim 등)
    - 6-12개월
      - 소규모 멀티 로봇(예: 3대 UGV 혹은 1 UGV + 1 드론) 시뮬레이션에서 분산/준-중앙집중식 SLAM 구현
      - 국내 학회에 논문 또는 포스터 한 편 정도를 목표로
  - 2년차: 멀티 로봇 + 군집/임무 계획까지 확장
    - 13-18개월
      - 센서 제약(제한 FoV LiDAR, 카메라 occlusion, 통신 dropout)을 넣은 시뮬레이션 환경 구성
      - 이 환경에서 robust loop closure, 통신량 최소화 전략, 분산 최적화 개선
    - 18-24개월
      - SLAM 결과를 사용해 정찰/감시 임무의 경로 계획·역할 분담 알고리즘 개발
      - 국제 학회 + 석사 논문 완성

### ✅ 결론

- 우선 생각한 3가지 방식을 교수님과 진지한 대화를 해보고 정확한 방향을 잡아야겠음
- 그리고 연구실 내에 쉽게 사용할 수 있는 데이터셋을 가지고 간단한 테스트로 SLAM 감을 잡아야겠음

<p><br></p>

---
