# A Potential Game-based Framework for Cooperative Driving at Mixed Un-signalized Intersections

**[Shiyu Fang](https://tops.tongji.edu.cn/info/1033/1190.htm)**, [Peng Hang](https://tops.tongji.edu.cn/info/1031/1383.htm), [Jian Sun](https://tops.tongji.edu.cn/info/1031/1187.htm)  

[Department of Traffic Engineering and Key Laboratory of Road and Traffic Engineering, Ministry of Education, Tongji University](https://tops.tongji.edu.cn/)  

## Abstract

Connected Autonomous Vehicles (CAVs) technology is believed to enhance traffic efficiency and safety significantly. However, numerous accidents have demonstrated that the decision-making algorithm of CAV under highly complex environments has limitations, especially at mixed intersections. Considering the increased hazards posed by heterogeneous Human Driven Vehicles (HDVs) in real-world traffic, an Adaptive Weight Shapley Weighted Potential Game (AWSW-PG) is proposed to establish a cooperative driving framework for CAVs. Heterogeneous HDVs are modeled by a non-cooperative Bayesian game and utilized as background traffic. Then, the potential game that connects the individual reward and cluster reward generates the optimal cooperative solution by searching the Nash Equilibrium of the problem. Furthermore, the Shapley value is introduced to quantify the unsymmetrical impact of each vehicle. Finally, given the uncontrollable and unpredictable nature of HDVs, an adaptive weight method is formalized to adjust the estimation on HDVs dynamically. To evaluate the effectiveness and robustness of the proposed cooperative driving framework, three cases are conducted. Results demonstrate that the AWSW-PG framework exhibits good performance in terms of efficiency and safety under different rates of penetration. In addition, the quantification of vehicle impacts and dynamic adjustment of HDVs estimates have been proven capable of guaranteeing stability and efficiency during cooperation.

## Method Overview

Firstly, based on our previous study, we formulate a non-cooperative Bayesian game to reproduce the heterogeneous HDVs decisions. Secondly, the individual reward and potential reward (cluster reward) are linked through Potential Games (PGs). Through rigorous derivation, we further demonstrate the uniqueness and global optimality of NE in PG. Then, the Shapley value is introduced to quantify the unsymmetrical impacts of vehicles. Finally, an adaptive weight method is proposed to dynamically correct the discrepancies between HDVs' real action and predicted action.  

![framework](./src/framework.png)

## Experiments
Multiple experiments are conducted, including an ablation experiment on the Shapley value in a purely CAV environment, a comparison of efficiency and safety under different Rates of Penetration (ROP), and the significance test after heterogeneous HDVs involved. Here we focus on a supplementary explanation of the results of the study and present them in a more intuitive manner (especially via .MP4). For further knowledge acquisition, please refer to [arXiv]().


### Ablation experiment on the Shapley value
In order to facilitate the reader to understand how Shapley value is constantly changing in the process of cooperation, we use the shade of color to represent the value of the Shapley value. More specifically, the closer the color of the vehicle is to purple, the higher its Shapley value is at this moment. This indicates that the vehicle currently has a greater impact on the system. Conversely, lighter colors indicate weaker impacts on the system. Additionally, each car's normalized Shapley value is displayed next to it. The cooperation case shown in Fig.5 in the paper is shown below  

<div align=center>
| <video muted controls width=380> <source src="./src/ablation-case.mp4"  type="video/mp4"> </video> |
</div>


### Comparison under different ROP
In this subsection, we compare the baseline and AWSW-PG(T=1) from an aggregate point of view at first. The results indicate that the implementation of the adaptive weight method provides efficient improvement for collision avoidance. A specific case comparison is shown below  

| <video muted controls width=380> <source src="./src/baseline-case1.mp4"  type="video/mp4"> </video> <video muted controls width=380> <source src="./src/AWSW-PG(T=1)-case1.mp4"  type="video/mp4"> </video> |

As observed in the video, collisions occur when CAVs are driven by the baseline model due to their inability to correct HDV estimates in real time. However, we acknowledge that driving is a sequential decision-making process, and selecting an appropriate planning time can effectively prevent shortsighted behavior. Moreover, in our paper, we mention that though the adaptive weight method successfully helps CAVs avoid collision, it sacrifices efficiency and causes deadlocks.

Thus, we have extended the planning horizon to 8 steps. Additionally, we also present a case to visualize this improvement 

| <video muted controls width=380> <source src="./src/AWSW-PG(T=1)-case2.mp4"  type="video/mp4"> </video> <video muted controls width=380> <source src="./src/AWSW-PG(T=8)-case2.mp4"  type="video/mp4"> </video> |

### Experiments with heterogeneous HDVs involved
Considering that CAVs will continually mix with HDVs that possess various driving abilities, and styles in a long time. we further investigate our model by introducing heterogeneous human-driven vehicles into the background traffic. Specifically, we use orange, blue, and green to represent aggressive, neutral, and conservative drivers respectively (unknown information for connected autonomous vehicles). The transparency of colors indicates the discrepancy between actual actions and predicted actions. When the discrepancy between actual and predicted actions is relatively minor, HDV will be marked with a √ symbol.


| <video muted controls width=380> <source src="./src/h-hdvs-case1.mp4"  type="video/mp4"> </video> <video muted controls width=380> <source src="./src/h-hdvs-case2.mp4"  type="video/mp4"> </video> |


## Citation
```
@misc{,
      title={}, 
      author={},
      year={2023},
      eprint={},
      archivePrefix={arXiv},
      primaryClass={cs.MA}
}
```

## Appendix

### 1.Modeling Heterogeneous HDV
Despite the uncertainty due to the absence of traffic lights, unpredictable and uncontrollable HV latent intention of decision may lead to even greater strait for CAVs. In order to validate the cooperative driving algorithm of CAVs in heterogeneous mixed traffic. In this section, sophisticated real-world drivers' demonstrations were extracted for reproducing heterogeneous HV decisions. 

The main process consists of four steps. Firstly, interaction data from a real-world intersection were collected. Secondly, drivers' decisions were classified into three groups by K-means cluster. Then, non-cooperative game, known as a promising model to reproduce the process of human decision making, was selected to guide the generation of HVs' decision. Finally, the decision-making preference of each group was calibrated through IRL. 

#### Drivers' Decisions Classification by K-means Cluster
In order to reproduce drivers with different decision-making preferences. The first priority was to determine how many decision clusters the drivers at the intersection of XXJH can be divided into. Based on the result of the elbow method, a simple but versatile theory to determine the number of clusters using the Sum of Squared Errors (SSE), three clusters work best for our data. Considering that speed and acceleration are the most intuitive manifestation of decision making during driving, the average, maximum, minimum, and standard deviation of speed and acceleration of vehicles were taken as the clustering parameters}. K-means clustering was then used to classify naturalistic human driving data samples in XXJH.

After the clustering algorithm converged, the drivers' decisions in XXJH were divided into three clusters: normal, conservative, and aggressive. Furthermore, their trajectories were used as expert demonstrations and then compared with HDVs' feasible trajectories to calibrate different decision-making preferences. In this paper, a non-cooperative game was chosen to estimate possible decisions human may adopt when confronted with other drivers because it achieves more realistic human behavior when performing conflicting maneuvers at intersections. Together with vehicle dynamics, feasible trajectories of each frame can be concluded.

#### HDVs' Feasible Trajectories Generation through Non-cooperative Game
As mentioned before, game theory describes human as a rational decision-maker who takes action dependencies into account. Hence, there is a growing application in the field of modeling human decision. In this paper, we regard human drivers as rational decision-makers and are aware of the consequence that their actions will influence other drivers who have conflict with them in temporal and spatial dimensions. Non-cooperative game was therefore established to mimic how drivers conjecture and compete with each other while driving in sharing space. We considered a sampling interval, $\Delta t=0.1s$, and an action set including six strategies that represent common driving maneuvers in urban traffic is listed below. 

#### Decision-making Preference Calibration by IRL
After dividing drivers into groups and generating feasible trajectories through non-cooperative game. IRL was introduced to excavate inherent characteristics that influence the expert decision. IRL was proposed later than behavior cloning. Though they share many similarities. Differing from simply imitating expert maneuvers, IRL tries to infer the reason why experts make their decision and then optimize the strategy. In other words, except directly learning the state-action mapping, IRL infers the form of reward weight and optimizes maneuvers through it. The pseudocode of maximum entropy IRL is summarized in Algorithm.1.

After training, the reward weights of different driver groups can be calibrated through maximizing entropy and iterating, as shown below.

As in Table, the aggressive driver group possessed the highest efficiency value, and lowest safety and comfort value, indicating their preference for passing at a high speed and more willingness to detour rather than stop and wait. Meanwhile, conservative drivers were more concerned about driving comfort and safety, leading to conservative decisions. The reward weights of normal drivers were in the middle range, these drivers do not have an over preference and try to balance efficiency, comfort, and safety while driving. 

#### Decision-making Preference Calibration by IRL

## Contact

If you have any questions, feel free to contact us (2111219@tongji.edu.cn).
