# A Game-based Framework for Cooperative Driving at Mixed Un-signalized Intersections

**[Yiming Cui](https://tops.tongji.edu.cn/info/1131/1818.htm)**, [Shiyu Fang](https://tops.tongji.edu.cn/info/1033/1190.htm), [Qian Chen](https://tops.tongji.edu.cn/info/1132/1806.htm), [Peng Hang](https://tops.tongji.edu.cn/info/1031/1383.htm), [Jian Sun](https://tops.tongji.edu.cn/info/1031/1187.htm)  

[Department of Traffic Engineering and Key Laboratory of Road and Traffic Engineering, Ministry of Education, Tongji University](https://tops.tongji.edu.cn/)  

## Abstract

During the ongoing development and proliferation of autonomous vehicles, human-driven vehicles (HDVs) and connected and automated vehicles (CAVs) will coexist in mixed traffic environments for the foreseeable future. However, current autonomous driving systems often face challenges in ensuring optimal safety and efficiency, particularly in complex conflict scenarios. To address these shortcomings and improve cooperation in mixed traffic environments, this paper presents a cooperative decision-making method based on game theory. The proposed framework accounts for both CAV-CAV collaboration and CAV-HDV interaction in mixed traffic at un-signalized intersections. this study introduces a parameter updating mechanism based on twin games to dynamically adjust HDVs' parameters to better predict and respond to variable human driving behaviors. To validate the effectiveness of the proposed cooperative driving framework, we compared its safety and efficiency with other established methods. The results demonstrate that our nethod successfully ensures both safety and efficiency in mixed traffic environments. Additionally, several validation experiments were conducted using a hardware-in-the-loop and human-in-the-loop experimental platform built on CARLA, confirming the practical applicability of the method.

## Method Overview

In terms of this complex conflict problem and realize safe and efficient cooperation in mixed traffic, we design a multi-vehicle cooperative decision-making method coupled with the interaction between CAVs and HDVs and the cooperation of CAVs based on game theory. 
For individual vehicles, we adopt a unified design of the utility function, taking into account the needs of safety, efficiency, and comfort. The total reward for an individual is represented as the weighted sum of three indices. The entire model is expressed as a bi-level optimization problem, structured such that the objective is to maximize the overall reward of cooperative CAVs, with constraints on maximizing the reward of each HDV.

Specifically, we proposed a cooperative decision-making model of the whole CAVs based on the cooperative game to achieve the decision action of CAVs. It is modeled as a single level constrained optimization problem to maximize the total rewards of CAVs. Security Hard constraints are designed to meet the most basic security guarantees between CAVs. The CAVs forming cooperative relationships need to satisfy a series of principles including individual rationality and group rationality.

Secondly, we establish an interaction model between CAV and HDV based on the Stackelberg game. In this part, we treat all CAV as a whole and build the model structure of leader-multi-followers. The model is modeled as a bi-level programming problem due to the general solving method of Stackelberg model. We designed parameters to characterize the differences in driving behavior between different human drivers and at different times in the interaction process. Moreover, we design the update rule of weight of HDV’s reward function based on the twin game, and realize the parameter adjustment to adapt to the dynamic interaction uncertainty of HDV. Security Hard constraints are designed to meet the most basic security guarantees between CAV and HDV.

Finally, to demonstrate the feasibility and effectiveness of the cooperative driving framework, cases are designed for experimental verification from multiple perspectives. We conduct the comparison of the simulation results with different methods which contains rule-based, reservation-based and reinforcement learning-based methods. Additionally, we did some validation experiments to verify the feasibility of method application including CAVs cooperative algorithm verification of domain controller in the loop and collaborative algorithm verification in mixed traffic of human driving in the loop.

![framework](./src/Framework.png)


## Simulation
<div align=center>
| <video muted controls width=380> <source src="./vedio/FIFO.mp4"  type="video/mp4"> </video> <video muted controls width=380> <source src="./vedio/Virtual-IDM.mp4"  type="video/mp4"> </video> |
</div>
Three kinds of methods that are reservation-based and reinforcement learning-based methods are designed based on the above environment, and the simulation results are compared with the proposed method. For the method in this paper, two cases are designed, respectively. 

### Case1-FIFO
Choose First in First Out (\textbf{FIFO}) method as one of the reservation-based method named \textit{Case1}. Specifically, only one vehicle at the same time is allowed to enter the designated area within a certain range of the intersection (in case design, the range within 10m before the stop line and the intersection conflict area). 
<div align=center>
| <video muted controls width=380> <source src="./vedio/FIFO.mp4"  type="video/mp4"> </video> |
</div>

### Case2-Virtual IDM
Virtual platoon projection method \cite{xu2018distributed} is designed as \textit{Case2}. This method converts the two-dimensional spatial position of a vehicle into a one-dimensional position by referring to the position of the conflict point between the two vehicles. The platoon formed after projection can calculate the longitude decision action according to the car-following model like IDM, called \textbf{Virtual-IDM}.
<div align=center>
| <video muted controls width=380> <source src="./vedio/Virtual-IDM.mp4"  type="video/mp4"> </video> |
</div>

### Case3-RL PPO
As for the reinforcement learning method, Proximal Policy Optimization (PPO) algorithm has high computational efficiency, can deal with continuous action space and discrete action space problems, simple implementation, wide application range. The baseline PPO algorithm provided in Stable-Baselines3 \cite{stable-baselines3} was selected as the comparison method as \textit{Case3}. And PPO interact and train the model in the environment provided by highway-env.
<div align=center>
| <video muted controls width=380> <source src="./vedio/RL-PPO.mp4"  type="video/mp4"> </video> |
</div>

### Case4-Proposed NonTwin
The parameters related to the weight of HDVs reward function are determined and updated by the twin game and the parameters are fixed which are always the initial ones.


<div align=center>
| <video muted controls width=380> <source src="./vedio/Proposed-Nontwin.mp4"  type="video/mp4"> </video> |
</div>

### Case5-Proposed InTwin
<div align=center>
| <video muted controls width=380> <source src="./vedio/Proposed-Intwin.mp4"  type="video/mp4"> </video> |
</div>

## Experiment

### Scenario-(1) Unprotected left turn of 2 CAVs
The first experiment involved a scenario of an unprotected left turn with two CAVs to verify the possibility of CAV cooperative algorithm deployment and application under purely CAVs. Approaching from opposite directions on a stretch of road, one vehicle proceeded straight while the other executed a left turn.
<div align=center>
 <iframe width="640" height="640" src="https://resource.onsite.com.cn/temp/cym/cym-vedio/2CAV-上帝/2CAV-上帝.mp4" title="2CAV-上帝" frameborder="0" allowfullscreen></iframe> 
</div>


<div align=center>
| <iframe width="320" height="240" src="https://resource.onsite.com.cn/temp/cym/cym-vedio/2CAV-hero1/2CAV-hero1.mp4" title="YouTube video player" frameborder="0" allowfullscreen></iframe>  <iframe width="320" height="240" src="https://resource.onsite.com.cn/temp/cym/cym-vedio/2CAV-hero3/2CAV-hero3.mp4" title="YouTube video player" frameborder="0" allowfullscreen></iframe> |
</div>


### Scenario-(2) Mixed traffic of 3CAV & 1HDV
In order to verify the effectiveness of the collaborative algorithm and the twin game in the mixed traffic scenario, the second experiment was conducted in the scenario of three CAVs and one HDV. Three subjects with different driving styles were selected to complete the driving task of HDV and interact with three CAVs in the designed scenario.

#### Driver1
<div align=center>
| <iframe width="275" height="275" src="https://resource.onsite.com.cn/temp/cym/cym-vedio/3CAV1HV-Case1-上帝视角/3CAV1HV-Case1-上帝视角.mp4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  <iframe width="366" height="275" src="https://resource.onsite.com.cn/temp/cym/cym-vedio/3CAV1HV-Case1-HV视角/3CAV1HV-Case1-HV视角.mp4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> |
</div>

#### Driver2
<div align=center>
| <iframe width="275" height="275" src="https://resource.onsite.com.cn/temp/cym/cym-vedio/3CAV1HV-Case2-上帝视角/3CAV1HV-Case2-上帝视角.mp4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  <iframe width="366" height="275" src="https://resource.onsite.com.cn/temp/cym/cym-vedio/3CAV1HV-Case2-HV视角/3CAV1HV-Case2-HV视角.mp4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> |
</div>

#### Driver3
<div align=center>
| <iframe width="275" height="275" src="https://resource.onsite.com.cn/temp/cym/cym-vedio/3CAV1HV-Case3-上帝视角/3CAV1HV-Case3-上帝视角.mp4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  <iframe width="366" height="275" src="https://resource.onsite.com.cn/temp/cym/cym-vedio/3CAV1HV-Case3-HV视角/3CAV1HV-Case3-HV视角.mp4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> |
</div>



## Contact

If you have any questions, feel free to contact us (2310796@tongji.edu.cn).
