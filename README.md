# AISL PROJECT

[![KR](https://img.shields.io/badge/README-한국어-blue)](./README.ko.md)
[![EN](https://img.shields.io/badge/README-English-red)](./README.md)

<img src="https://capsule-render.vercel.app/api?type=waving&color=413fd9&height=150&section=header&text=Getting%20ready...&fontSize=35" />

## 🧠 About AISL PROJECT

### 🎯 Main Objectives

### 🧰 Tools

### 🛠 Tech Stack
**Languages**  
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=Python&logoColor=white)

<p><br></p>

---

## March 10, 2026

### 📝 To-Do (03/10/2026)

- [] A serious interview with the professor (regarding the selection of personal research topics)
- [] SLAM testing based on public datasets in the lab

### 📌 Notes

- 

### ✅ Conclusion

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
  - Based on this, try to compress about three topics that fit well into the defense company robot/unmanned system and are good for thesis and portfolio
  1. Distributed Multi-Robot SLAM: Without a central server (or least dependent), robots pose with partial maps, and distributed or quasi-distributed SLAMs that gradually match global maps in the event of communication loss or delay
  2. Robust Multi-Robot SLAM: Multi-SLAM cooperatively increases recognition performance under sensor treaty conditions common in defense environments such as limited FoV LiDAR, noisy IMU, camera obscuration, etc
  3. Multi-robot SLAM based cluster mission planning (MUM-T in mind): a study that connects multi-SLAM results (shared maps, uncertainty of each robot) directly to cluster path planning, exploration, and surveillance mission assignments
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
