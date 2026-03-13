# AISL's journey

[![KR](https://img.shields.io/badge/README-한국어-blue)](./README.ko.md)
[![EN](https://img.shields.io/badge/README-English-red)](./README.md)

<img src="https://capsule-render.vercel.app/api?type=waving&color=413fd9&height=150&section=header&text=Until%20the%20day%20I%20get%20a%20job%20at%20the%20company%20I%20want%20to%20go%20to...&fontSize=32" />

## 🧠 About AISL PROJECT

### 🎯 Main Objectives

### 🧰 Tools

### 🛠 Tech Stack
**Languages**  
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=Python&logoColor=white)

<p><br></p>

---

## March 13, 2026

### 📝 To-Do (03/12/2026)

### 📌 Notes

### ✅ Conclusion

<p><br></p>

---

## March 12, 2026

### 📝 To-Do (03/12/2026)

- [X] Test the OpenVINS algorithm

### 📌 Notes

- I used the data set provided by EuRoC, but I couldn't find it at this point, so I tested it based on the public data provided by KITTI, but I couldn't see anything on the rviz screen and continuous error on the terminal running the launcher file
  - The cause of the problem shows that the KITTI dataset violated static initalization conditions due to initial operation with [Init]: failed static init: platform moving too much, and the original calibration value of KITTI is different from the Kalibr format used by OpenVINS. It does not just change the name of the topic, but if the tranformation matrix (T) between the acceleration/gyro noise model for KITTI and the camera-IMU is not directly calculated and inserted, the filter will immediately diverge
- While I was combing through the tutorials provided by OpenVINS, the data(ros1 cannot be downloaded at this time, https://docs.openvins.com/gs-datasets.html <- conference) can be downloaded as a zip file. There is a command that can convert the ros2 file to ros1 after downloading, so I converted it and tested it successfully

### ✅ Conclusion

- Test with a dataset other than the one we did today
- Study OpenVINS accurately

<p><br></p>

---

## March 11, 2026

### 📝 To-Do (03/11/2026)

- [X] SLAM testing based on public datasets
- [X] Reading the papers I received from the professor

### 📌 Notes

- If I switch to Visual SLAM based, what I want is ORB-SLAM, but I decided to test this first by recommending the OpenVINS project to lab member who has experience in switching to Visual SLAM based because there are many dependence problems during installation (https://github.com/rpng/open_vins <- Reference)
  - It was very difficult because I experienced several out-of-memory problems in the middle, but I successfully ran OpenVINS simulation
  - The two screens after completion of the drive are performance indicators and visualization results showing how accurately OpenVINS estimates the robot's movement(trajectory)
  - First Image : Trajectory visualization (a drawing of the robot's path on a 2D plane)
  - Second Image : estimation accuracy (a ddta window that numerically shows "how different is the position I calculated from the real thing?" as the simulation goes back to real time)
<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/Trajectory%20Visualization.jpeg" width="250"/>
<img src="https://github.com/Kim-SeongGeon/AISL/blob/main/Image/Estimation%20Accuracy.png" width="250"/>

- The paper received from the professor presents a non-repetitive VSLs-based technique that significantly improves the accuracy and efficiency of feature map merging in multi-robot systems, which makes an important contribution to real-time robot system implementation

### ✅ Conclusion

- Proceed with what to do after the OpenVINS project
- Continue reading VSLs-based technical papers

<p><br></p>

--- 

## March 10, 2026

### 📝 To-Do (03/10/2026)

- [X] A serious interview with the professor (regarding the selection of personal research topics)
- [X] SLAM testing based on public datasets

### 📌 Notes

- The professor also liked the topics I thought of and gave me advice on the second one because another lab member is doing it, so I will proceed with the 1st and 3rd in a good relationship
  - In the first topic, the 'communication constraint' condition lacks a lot of knowledge in the field of communication and thus passes (or changes to some constraint)
  - Take the first topic as the main subject and expand it to the third topic, the third is the master's papers, and the mission plan is not to use AI
  - Sparse(including feature) Map Merging appears to be a necessary and practical study in the commercial and defense sectors
  - The test starts with the simulation(Matlab, etc.) with the algorithm as important
  - Catch the baseline well
  - Try ICP+VSLs combination well
  - Geometric information (location information of landmarks) + class information
- I tried SLAM test based on public dataset, but I ran into a lot of unexpected problems and asked for help from Lab member who studied about it tomorrow

### ✅ Conclusion

- Read and study the papers that the professor sent and recommeded
- Tomorrow, learn SLAM test based on public dataset and make sure it's mine

<p><br></p>

---

## March 09, 2026

### 📝 To-Do (03/09/2025)

- [X] Research to choose an accurate personal research topic

### 📌 Notes

- I have received a multi-robot project that I have been doing since I was an undergraduate research student in the first year of my master's project, so I think I should conduct personal research in this field       
- Since employment in a defense company is my ultimate goal, I investigate what kind of SW, R&D talent I want from a defense company should select to enter the company and do it well
  - If I think about employment first, you need to understand C++/Python-based algorithm implementation capabilties, practical projects and papers related to 'unmanned/robot', and practical SW architectures that can be implanted in various robot platforms (e.g., 4th leg on the ground, UGV, USV, etc.)
  - Environmental characteristics considered when using multi-robot SLAM in defence or battlefield include GNSS vulnerability (indoor, underground, disaster/electric field, electronic warfare environment), communication delay and disruption (distributed and robust SLAM and clustering required), mixing multiple heterogeneous robots (four-legged walking, UGV, drone, USV, etc.) and sensor restrictions or partially obscured (smoke, dust, dark environment, limited FoV LiDAR, etc.)
  - Among them, if the thesis and demonstration are implemented within 2 years of the master's degree, 'Distributed Multi-Robot SLAM and Reconnaissance Mission Plan Considering Communication and Sensor Constraints' is a big topic, and SLAM is attached in the 1st year and mission plan/group is appropriate in the 2nd year
 
- Brief Master's 1st to 2nd Year Roadmap (Research + Job Preparation)
  - Year 1: Laying the foundation + 1 paper level results
    - 0-6 Months
      - Theoretical/Code: Practice analyzing and implementing a multi-robot SLAM system verified such as ORB-SLAM series, pose graph SLAM, and LAMP/LAMP2.0
      - Language/Tools: C++/Python, ROS2, Git, Basic PCL/OpenCV/Robot Simulator (Gazebo/Ignition, Isaac Sim, etc.)
    - 6-12 Months
      - Distributed/semi-centralized SLAM implementation in small multi-robot (e.g., three UGVs or one UGV + one drone) simulations
      - Aiming to write a paper or poster to a Korean society
  - Year 2: Expanding to Multi-Robot + Cluster/Mission Plan
    - 13-18 Months
      - Configuring a simulation environment with sensor constraints (limited FoV LiDAR, camera occlusion, communication dropout)
      - Improve robust loop closure, traffic minimization strategies, and distributed optimization in this environment
    - 18-24 Months
      - Development of route planning and role-sharing algorithms for reconnaissance/monitoring missions using SLAM results
      - International conference + Master's thesis completion

### ✅ Conclusion

- First of all, I will have a serious conversation with the professor about the three ways I thought and find the exact direction
- And with a dataset that can be used easily in the laboratory, I need to get a sense of SLAM with a simple test

<p><br></p>

---
