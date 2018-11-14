[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135623-e770e354-7d12-11e8-998d-29fc74429ca2.gif "Trained Agent"

# udacity_project_tennis

## Project Details

This document is the report of the third Udacity project (Collaboration and Competition) for deep reinforcment learning. 

For this project, I have trained a single DDPG meta-agent which controlls both agents, using the [Tennis](https://github.com/Unity-Technologies/ml-agents/blob/e82450ab8304093871fd19b876a0f819d390e79d/docs/Learning-Environment-Examples.md#tennis) environment.

![example tennis][image1]

In this environment, two agents control rackets to bounce a ball over a net.
If an agent hits the ball over the net, it receives a reward of +0.1.
If an agent lets a ball hit the ground or hits the ball out of bounds, it receives a reward of -0.01.
Thus, the goal of each agent is to keep the ball in play.

The observation space consists of 8 variables corresponding to the position and velocity of the ball and racket.
Each agent receives its own, local observation.
Two continuous actions are available, corresponding to movement toward (or away from) the net, and jumping.

The task is episodic, and in order to solve the environment, the agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents).
Specifically,

* After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 2 (potentially different) scores. We then take the maximum of these 2 scores.
* This yields a single score for each episode.
The environment is considered solved, when the average (over 100 episodes) of those scores is at least +0.5.

## Implementation

The single DDPG agent is inspired by the [bi-pedal DDPG soution](https://github.com/udacity/deep-reinforcement-learning/blob/master/ddpg-bipedal/ddpg_agent.py) with the following adaptations:

* The OU noise has an additional noise decay factor (like epsilon-greedy), to reduce the influence of the noise on the agents actions
* Two agents are controlled by one meta-agent by concatenating both observation and action vectors
* Only the informed immediate reward (i.e. reward not equal 0.0) is stored to the replay buffer

## Getting Started

### Install Instructions

* Please follow the [instructions in the DRLND GitHub repository](https://github.com/udacity/deep-reinforcement-learning#dependencies) to set up a Python environment.
* By following these instructions, you will install PyTorch, the ML-Agents toolkit, and a few more Python packages required to complete the project.
* Put all files into the `p3_collab-compet/` folder

### Run the Report

Run the [Report.ipynb](Report.ipynb) which realizes the training in a Actor-Critic DDPG setup and solves the task in 3404 iterations.


## Future Ideas

This implementation realizes a single DDPG meta-agent with free communication.
Therefore, only a single actor and a single critic have been implemented where the observations of both agents have been concatenated and stored to the replay buffer.
However, more sophisticated multi-agent approaches with multiply actors cold also be implemented as well [MADDPG](https://github.com/openai/maddpg).
Furthermore, approaches like A2C or A3C could lead to a more stable training, since the achived scores highly depends on the drawn random seeds.
