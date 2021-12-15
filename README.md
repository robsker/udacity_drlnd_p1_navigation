[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135619-d90f2f28-7d12-11e8-8823-82b970a54d7e.gif "Trained Agent"

# Project 1: Navigation

### Goal

The goal of this project is to train an agent to navigate a large, square world, collecting yellow bananas, while learning to avoid the blue banana obstacles.

![Trained Agent][image1]

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana.  Thus, the goal of this agent is to collect as many yellow bananas as possible while avoiding blue bananas.  

The task is episodic, and in order to solve the environment, your agent must get an average score of +13 over 100 consecutive episodes.

### State Space
The state space has 37 dimensions, some of which are discrete spaces, while others are continuous. The state space contains the agent's velocity, along with ray-based perception of objects around agent's forward direction. 

### Action Space
Given this state-space information, the agent has to learn how to best select actions.  Four discrete actions are available, corresponding to:
- **`0`** - move forward.
- **`1`** - move backward.
- **`2`** - turn left.
- **`3`** - turn right.

### Getting Started

1. Download the environment from one of the links below.  You need only select the environment that matches your operating system:
    - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux.zip)
    - Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana.app.zip)
    - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86.zip)
    - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86_64.zip)
    
    (_For Windows users_) Check out [this link](https://support.microsoft.com/en-us/help/827218/how-to-determine-whether-a-computer-is-running-a-32-bit-version-or-64) if you need help with determining if your computer is running a 32-bit version or 64-bit version of the Windows operating system.

    (_For AWS_) If you'd like to train the agent on AWS (and have not [enabled a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md)), then please use [this link](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux_NoVis.zip) to obtain the environment.

2. Place the file in the `p1_navigation/` folder, and unzip (or decompress) the file. 

### Instructions

After downloading the Banana.app mentioned above, start your `drlnd` conda virutal environnment, and launch the Jupyter notebook with the `jupyter-notebook` command from this folder on the command line.

#### (Optional) Create drlnd Conda Environment

If you have not previously built a `drlnd` conda environment, please refer to the following document, which will take you through the steps to create it:
[https://github.com/robsker/deep-reinforcement-learning#dependencies](https://github.com/robsker/deep-reinforcement-learning#dependencies)

#### Running from Saved Weights
If you would rather run from the previously saved weights only (ie, you don't want to actually take the time to re-train the agent on your own), you can run the following sections of the jupyter-notebook exclusively:
* #1 Start the Environment
* #5 Run the Saved Weights!

You should be able to see a trained agent move throughout the environment, collecting yellow bananas, while simultaneously avoiding the blue bananas.

