# Report

## Proximal Policy Optimization (PPO) Algorithm

Proximal Policy Optimization, or PPO, is a policy gradient method for reinforcement learning. This algorithm alternates between sampling data
through interaction with the environment, and optimizing a "surrogate" objective function using stochastic gradient ascent. The PPO PPO can outperform other online policy gradient methods,
and overall strikes a favorable balance between sample complexity, simplicity, and wall-time.

In this project there are 20 agents and so the PPO is able to use multiple (non-interacting, parallel) copies of the same agent to distribute the task of gathering experience.

The Network Architecture used in this project has the following configuration:

- A Gaussian Actor Critic Network:  which consists of 2 networks: the actor network and the critic network.
- the input layers of the two networks are linear layers with an input size of 33 (state dimension), and output of 64
- the second layer of both networks has an input size of 64 and output of 64
- the output layer of the action network has 64 inputs and 4 outputs (action dimension)
- the output layer of the critic network has 64 inputs and 1 output
- Both the actor and the critic networks use tanh activations
    
    ![image](https://user-images.githubusercontent.com/46076665/110048960-e1758b80-7d1e-11eb-9b95-79b70d2f30a9.png)


The training hyperparameters used are:
- optimizer function: Adam(3e-4, eps=1e-5)
- actor optimizer function: Adam(3e-4)
- critic optimizer function: Adam(1e-3)
- discount: 0.99
- generalized advantage estimation (gae) tau: 0.95
- gradient clip: 0.5
- rollout length: 2048
- optimization epochs: 10
- mini batch size: 64
- ppo ratio clip: 0.2
- log interval: 2048
- max_steps: 2e7
- target kl: 0.01

## Results

![image](https://user-images.githubusercontent.com/46076665/109899849-749dbb00-7c64-11eb-81dd-698eb7235a5f.png)

The task was solved in 180 episodes i.e. the agent is able to receive an average reward (over 100 episodes, and over all 20 agents) of at least +30 within 180 episodes.

## Future ideas for improving the agent's performance
- Try a different algorithm such as the A3C or D4PG
- Tune the hyperparameters such as the optimizer functions, clipping thresholds and regularization hyperparameters
- Use a new clipping function to support a rollback behavior to restrict the difference between the new policy and the old one such as in this [paper](https://arxiv.org/abs/1903.07940)
