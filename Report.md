[//]: # (Image References)

[image1]: https://github.com/drewmitchner/Udacity_DeepRL_Project1_Navigation/blob/main/Banana_Navigation_ScorePerEpisode.PNG "Learning Plot"

# Navigation Project Report

### Summary

In this project, Deep Q-Learning was used to solve the Banana environment in Unity. In the environment, the agent received a reward of +1 for collecting a yellow banana and a reward of -1 for collecting a blue banana. Each episode ended automatically after 300 timesteps and not before then. The observation space had a size of 37, which included the agent's velocity and a ray-tracing representation of its perception. At each timestep the agent could choose between 4 options:

1. Move Forward
2. Move Back
3. Turn Left
4. Turn Right

### Learning Algorithm

The agent was trained using a Q-Learning algorithm, with state-action pairs used to estimate the Q-value. A deep neural network was used to give a nonlinear estimate of the state-action values.

The Q-learning algorithm made use of Q-targets to assist with training and prevent the algorithm from trying to hit a moving target. The learning step was executed every 4 steps. A batch of 64 experiences used for learning were pulled randomly from a batch of the most recent 10,000 timesteps. 

For the deep neural network, a set of 3 fully-connected layers mapped the state-space (37) to the action-space (4). The first fully-connected layer went from size 37 to 64, the second layer from size 64 to 64, and the third from size 64 down to 4.

A full list of the training hyperparameters is shown below:

- tau: 0.001 (for the soft-update of the target parameters)
- Buffer Size: 10,000 (number of past experience replays)
- Batch Size: 64 (Number of experiences learned from each learning step)
- Gamma: 0.99 (Discount factor)
- Alpha: 0.0006 (Learning rate)
- Update Every: 4 (Interval between learning steps)
- FC1_out = 64 (Output of first fully connected layer)
- FC2_out = 64 (Output of second fully connected layer)

The hyperparameters used were similar to those used for the DQN-lesson excersize. I attempted manually tuning them by hand and found these to give the best results. More attention to the selection of the hyperparameters would lead to improved results.

### Results

A plot of score per episode shows how the agent learned over time.

![Learning Plot][image1]

After 800 episodes the agent was able to achieve an average score of +15.46 over 100 episodes. The agent took about 540 episodes to reach an average score of +13 over 100 episodes, the threshold at which the environment was deemed "solved".

### Future Work

The training algorithm presented here demonstrates a basic implementation of the DQN algorithm using Q-Targets and experience replay to assist in training. To improve learning performance, additional techniques such as dueling-networks, prioritized replay, or double-DQN could be employed. After looking through some of the student questions in the knowledge forum, there seemed to be a consensus that these techniques were not able to produce noticeable improvements in performance.

As typical for neural networks, a more complicated network consisting of larger and/or more hidden layers may be able to improve performance. Additionally, as was suggested as the bonus challenge for this project, a network using the 84x84 pixels as the state-space rather than the ray-tracing representation may be able to improve performance since a more full picture of the environment is available to the agent in order to make a better decision. Both of these suggested improvements to tradeoff complexity with training time.
