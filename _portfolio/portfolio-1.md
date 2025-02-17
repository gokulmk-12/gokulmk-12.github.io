---
title: "Dynamic Swarm Navigation"
excerpt: "Multi-Agent RL for Dynamic Swarm Navigation<br/><img src='/images/project1_1.png'>"
collection: portfolio
---

<span style="font-size: 17px;">
This project was undertaken as part of <b>Inter-IIT Tech Meet 13.0</b> at <b>IIT Bombay</b>, based on a problem statement provided by Kalyani Bharatforge. Titled <b>"Centralized Intelligence for Dynamic Swarm Navigation,"</b> the project aimed to develop an effective approach for swarm navigation in continuously evolving environments.
</span>

<div class="figure-container">
  <img src="/videos/project1_1.gif" alt="Small Swarm Navigation" width="100%">
  <p style="text-align: center; font-style; font-size: 15px;">Figure 1: Small Swarm Navigation</p>
</div>

<div style="text-align: center;">
    <img src="/videos/project1_2.gif" alt="Large Swarm Navigation" width="100%">
    <p style="text-align: center; font-style; font-size: 15px;">Figure 2: Large Swarm Navigation</p>
</div>

### Introduction
<span style="font-size: 17px;">
One of the essential technologies for creating smart robot swarms is motion planning. Traditional path planning methods in robotics require
precise localization and complete maps, limiting their adaptability in dynamic environments. Reinforcement learning (RL), especially deep reinforcement learning (DRL), has emerged as a key strategy to address such issues.
</span>

### Simulation
<span style="font-size: 17px;">
The simulation framework is developed in <b>Gazebo</b> Classic and integrated with <b>ROS 2 Humble</b>. Each robot carries a 2D LiDAR sensor used for obstacle detection. Robots are deployed at random positions in the environment, and their initial configurations are defined in a YAML file.
</span>

<div style="text-align: center;">
    <img src="/images/project1_5.png" alt="Reward Plot" width="100%">
    <p style="text-align: center; font-style; font-size: 15px;">Figure 3: Illustration of Process Flowchart</p>
</div>

### Reinforcement Learning
<span style="font-size: 17px;">
The navigation task is formulated as a <b>Markov Decision Process (MDP)</b> represented by the tuple (S, A, S′, P, R), where each element holds its standard interpretation.
<span>

### State Space  

<ul style="font-size: 17px; line-height: 1.6;">
  <li><strong>Normalized Laser Scan Values</strong>: Measurements from the LiDAR, scaled to a normalized range.</li>
  <li><strong>Normalized Goal Distance to Arena Size Ratio</strong>: The distance to the target goal, normalized relative to the size of the navigation area.</li>
  <li><strong>Normalized Goal Heading Angle</strong>: The angle between the agent’s orientation and the direction to the goal, scaled to a normalized range.</li>
  <li><strong>Previous Linear Velocity</strong>: The linear velocity of the agent during the prior time step.</li>
  <li><strong>Previous Angular Velocity</strong>: The angular velocity of the agent during the prior time step.</li>
</ul> 

### Action Space  
<ul style="font-size: 17px; line-height: 1.6;">
  <li><strong>Linear velocity</strong>: Bounded between [-1, 1]</li>
  <li><strong>Angular velocity</strong>: Bounded between [-2, 2]</li>
</ul>

### Reward Function  
<ul style="font-size: 17px; line-height: 1.6;">
  <li><strong>Goal Alignment Penalty</strong>: A penalty applied for deviations in the heading angle from the optimal trajectory toward the goal.</li>
  <li><strong>Excessive Angular Velocity Penalty</strong>: Penalizes the agent for executing abrupt or excessively large angular velocity actions.</li>
  <li><strong>Proximity-to-Goal Reward</strong>: A reward inversely proportional to the Euclidean distance from the agent to the goal, encouraging progress toward the target.</li>
  <li><strong>Obstacle Proximity Penalty</strong>: A penalty incurred when the agent approaches obstacles, discouraging unsafe trajectories.</li>
  <li><strong>Excessive Linear Velocity Penalty</strong>: Penalizes the agent for employing large linear velocities that may compromise safety or stability.</li>
</ul>

### RL Algorithm
<span style="font-size: 17px;">
The primary RL navigation framework is implemented using the <b>Twin Delayed Deep Deterministic Policy Gradient</b> (TD3) algorithm. TD3 is an advanced off-policy RL algorithm. The key reasons for selecting TD3 over alternative baseline algorithms are 
</span>
<ul style="font-size: 17px; line-height: 1.6;">
  <li><strong>DDPG</strong> revealed a significant overestimation of Q-values, ultimately leading to policy degradation.</li>
  <li><strong>PPO</strong> is computationally intensive and sample inefficient as compared to off-policy algorithms for large-scale navigation tasks.</li>
  <li><strong>SAC</strong> and <strong>TD3</strong> have the best data efficiency. However, SAC trains a stochastic policy, which does not guarantee convergence to a single optimal solution.</li>
</ul>

### Methodology
<span style="font-size: 17px;">
The task was implemented as <b>Decentralized Training and Decentralized Execution (DTDE)</b>. Initially, a single agent (robot) is trained within a dynamic environment. The trained networks are then deployed across multiple instances, corresponding to the number of robots.
</span>

### Experiment and Simulation Results

<div style="text-align: center;">
    <img src="/images/project1_2.png" alt="Reward Plot" width="100%">
    <p style="text-align: center; font-style; font-size: 15px;">Figure 4: DDPG v/s TD3 Reward Plot</p>
</div>

<div style="text-align: center;">
    <img src="/images/project1_3.png" alt="Training Status" width="100%">
    <p style="text-align: center; font-style; font-size: 15px;">Figure 5: DDPG v/s TD3 Episodic Status Plot</p>

<div style="text-align: center;">
    <img src="/images/project1_4.png" alt="Training Status" width="100%">
    <p style="text-align: center; font-style; font-size: 15px;">Figure 6: DDPG v/s TD3 Robot Distance Travel Plot</p>
</div>
