# Deep Warlight AI Bot

We developed a deep neural network (DNN) based AI bot for the Warlight game. It applied an evolutionary strategy to evolve the weights of the DNN.

## Design Overview

Our DNN based AI bot includes the following modules. The DNN based AI bot includes three modules, which are the DNN module, the Bot module, and the Evolutionary Strategy module. The DNN module, written in java, works as the analysis core for this system, it evaluates the orders and actions for the Bot module. The Bot module, also written in java, is designed to receive orders from the DNN module, and take actions on the warlight board. The Evolutionary Strategies module, written in MATLAB, is used to evolve the weights of the connections between different layers of the DNN. 

![image](https://github.com/passionguan/Deep_Warlight_AI_Bot/blob/master/Figures/Design_Flow.png)

## Deep Neural Network Based Evaluation Function

DNN Module: The structure of this module is shown as follows. Our DNN contains four layers: the input layer and hidden layer 1 have 42 nodes, which represent the 42 regions on the warlight board. Hidden layer 2 has 6 nodes, which represent the 6 continents. The output layer has 1 node, which represent the output of the DNN.

The connections between the input layer and hidden layer 1 are constructed from the real connections of the regions on the warlight board. Each of the region on the warlight board represents a node in the hidden layer 1. The connections between the region and the neighbored regions are represented by the connections between the input layer nodes and the hidden layer 1 nodes. Each of these connections has a weight. The connections between hidden layer 1 and hidden layer 2 are constructed on continents. Each node from hidden layer 1 has only one connection to the nodes in hidden layer 2. The output layer includes only one node, which represent the outcome of the DNN.

![image](https://github.com/passionguan/Deep_Warlight_AI_Bot/blob/master/Figures/deep_neural_network.PNG)

## Example

The following figure shows the example of hidden layer 1. The connected regions shown in the board are represented as the connected nodes between the hidden layer 1 and hidden layer 2 in the deep neural networks. 

![image](https://github.com/passionguan/Deep_Warlight_AI_Bot/blob/master/Figures/Example_1.png)

The following figure shows an example of hidden layer 2. The regions that belong to the same continent are connected to the node which represents that continent. For instance, all the regions in the North America (red circle) are connected to the node in hidden layer 3 which represents the North America.

![image](https://github.com/passionguan/Deep_Warlight_AI_Bot/blob/master/Figures/Example_2.png)

## Tuning Parameters of DNN Using Covariance Matrix Adaptation Evolution Strategy (CMAES)

We use the CMAES to evolve the weights of the deep neural networks, because CMAES does not utilize any sort of crossover which would have to be specially designed to work with deep neural networks. The main components of the CMAES are shown as follows:

### Representation: Real-value

We use the real-value representation to evolve the weights of the deep neural networks, since these weights are real numbers.

### Fitness: Tournament

The fitness is determined by a round robin tournament. All 10 members of the population will play a game against each other member. They will get a number of points equal to the areas they control at the end of the game. If they win then they will get 42 (for the number of areas in the game) + 100 (the max number of rounds) – the number of rounds played. The scores overall games played are used as the fitness.

### Population: 10

We set the population to be 10 since this is a reasonable number as the tradeoff between the running time and evolved results. Because of the way the tournaments were set up each additional member of the population adds a significant amount of time.

### Recombination/Mutation: Add a random vector, a perturbation with zero mean

We add a random vector, a Gaussian perturbation with zero mean to perform the mutation operator. This is standard for CMAES which adjusts the standard deviation of this Gaussian. 

### Survivor Selection: Deterministic
### Parent Selection: Fitness proportional

Only 5 survivors are used. These survivors are combined using a weighting determined by the CMAES and the fitness of the functions.

### Initialization: Uniform Random [0,1]

We generate the random real numbers from [0, 1] to initialize the individuals of the population.

### Termination: Max number of generations = 1000

We set the max number of generations to be 1000 for the termination condition.

## Performance of the Deep Warlight AI Bot

Our evolved bot can outperform most of the low-level bots in the Warlight AI game. The evolved bot ranks the best in the Marquette University Institutes in terms of Elo. This may be biased by the amount of time that the bot was on the Warlight AI challenge server. More details please refer to 

http://theaigames.com/competitions/warlight-ai-challenge/leaderboard/global/a/kevin

## Authors and Copyright

Deep Warlight AI Bot is developed by Greg Merkel (
gregory.merkel@marquette.edu), Wenkai Guan   (wenkai.guan@marquette.edu).

Copyright (C) 2018, Marquette University.

