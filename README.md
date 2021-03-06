# DeepRL
Highly modularized implementation of popular deep RL algorithms by PyTorch. My principal here is to
reuse as much components as I can through different algorithms, use as less tricks as I can and switch
easily between classical control tasks like CartPole and Atari games with raw pixel inputs.

Implemented algorithms:
* Deep Q-Learning (DQN)
* Double DQN
* Dueling DQN
* Async Advantage Actor Critic (A3C)
* Async One-Step Q-Learning
* Async One-Step Sarsa 
* Async N-Step Q-Learning

# Curves
> Curves for CartPole are trivial so I didn't place it here.
## DQN, Double DQN, Dueling DQN 
![Loading...](https://raw.githubusercontent.com/ShangtongZhang/DeepRL/master/images/DQN-breakout.png)
![Loading...](https://raw.githubusercontent.com/ShangtongZhang/DeepRL/master/images/DQN-Pong.png)

The network and parameters here are exactly same as the [DeepMind Nature paper](https://www.nature.com/nature/journal/v518/n7540/full/nature14236.html). 
Training curve is smoothed by a window of size 100. All the models are trained in a server with
Xeon E5-2620 v3 and Titan X. For Breakout, test is triggered every 1000 episodes with 50 repetitions.
In total, 16M frames cost about 4 days and 10 hours. For Pong, test is triggered 
every 10 episodes with no repetition. In total, 4M frames cost about 18 hours.

## A3C

![Loading...](https://raw.githubusercontent.com/ShangtongZhang/DeepRL/master/images/A3C-PongNoFrameskip-v3.png)

The network I used here is same as the network in DQN except the activation function 
is **Elu** rather than Relu. The optimizer is **Adam** with non-shared parameters.
To my best knowledge, this network architecture is not the most suitable for A3C. 
If you use a 42 * 42 input, add a LSTM layer at last, you will get **much much much** better training speed 
than this. [GAE](http://www.breloff.com/DeepRL-OnlineGAE/) can also improve performance.

The first 15M frames took about 5 hours (16 processes) in a server with two Xeon E5-2620 v3.
This is the test curve. Test is triggered in a separate deterministic test process every 50K frames.

# Dependency
* Open AI gym
* PyTorch
* PIL (pip install Pillow)
* Python 2.7 (I didn't test with Python 3)

# Usage
Detailed usage and all training details can be found in ```main.py```

# References
* [Human Level Control through Deep Reinforcement Learning](https://www.nature.com/nature/journal/v518/n7540/full/nature14236.html)
* [Asynchronous Methods for Deep Reinforcement Learning](https://arxiv.org/abs/1602.01783)
* [Deep Reinforcement Learning with Double Q-learning](https://arxiv.org/abs/1509.06461)
* [Dueling Network Architectures for Deep Reinforcement Learning](https://arxiv.org/abs/1511.06581)
* [Playing Atari with Deep Reinforcement Learning](https://arxiv.org/abs/1312.5602)
* [HOGWILD!: A Lock-Free Approach to Parallelizing Stochastic Gradient Descent](https://arxiv.org/abs/1106.5730)
* [transedward/pytorch-dqn](https://github.com/transedward/pytorch-dqn)
* [ikostrikov/pytorch-a3c](https://github.com/ikostrikov/pytorch-a3c)
