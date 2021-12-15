# Summary
This file will describe the underlying functionality and architecture of the NN used for the DRL training.

## model.py
`model.py` contains the definition of the neural network used for the Q Action Value function approximation. The object exposed is called QNetwork.

### QNetwork Architecture
The QNetwork neural network is written in pytorch and consists of the following layers:
1. Input Layer with size 37. This is the size of the State Space that is used as the input.
2. First Hidden Layer (size 64) with Relu activation.
3. Second Hidden Layer (size 64) with Relu activation.
4. Output Layer with size 4. This is the size of the Action Space, the output of which represents the predicted value of the corresponding action at the input state.

### Agent Architecture and Functionality
The Agent consists of 2 QNetworks, one for training (`qnetwork_local`), while the other is for representing currently-predicted targets and calculating losses (`qnetwork_target`).

The Agent also makes use of a Replay Buffer, 485 in size, defined in the ReplayBuffer class and stored in the Agent's memory data.

#### act method
The `act` method is the core Agent method that returns an epsilon-greedy Action to take at the specified State. 

If a Random number is greater than the specified epsilon, it will calculate Q Action Values, as specified by the `qnetwork_local` QNetwork given the State input, and returns the Action with the max Q Value (the greedy Action).

Alternatively, if the Random number is less than epsilon, it will simply return a Random Action to take.

#### step method
Once an Action is chosen for the Agent to take at the particular State, as calculated and returned from the `act` method, the Agent is ready to step.

**Note:** The Agent actually steps in the environment by use of the `UnityEnvironment`'s API, in particular by calling:
```
env.step(action)[brain_name]
```

This call returns an `env_info` variable, via which the `next_state`, `reward`, and `done` are obtained.

See the `Navigation.ipynb` for the implementation.

Once the Agent has stepped inside the `UnityEnvironment`, you can call the Agent's `step` method, which does 2 things, namely:
1. Stores the (S, A, R, S′, done) tuple in the ReplayBuffer `memory`.
2. Every UPDATE_EVERY (4) timesteps (`t_step`), the Target Network is trained using random samples from the ReplayBuffer.

#### Training
The network training is done in a Sarsamax-like fashion in the `learn` method, where the Target Network is used to generate the target sums of the next_states and rewards (with respect to the gamma learning variable), while the Local Network is used to generate the value of the States.

Since the value of States should utimately approach the value of the Reward, plus the value of the Next State, the error (Mean Square Error, in particular) is calculated as the difference between the calculated Target and Local values.

Once the loss has been backward propogated to the Local Network using Adam Optimizer, the new weights in the Local Network are then copied out to the Target Network in the `soft_update` method.

### Plot of Rewwards
Reference the `Navigation.html` file to view the plot of rewards over time.

**Note:** It takes around 400 episodes, at 2000 max time steps each, to achieve the desired average of 13 reward points.

### Hyperparameters
I found I liked the results of allowing more time steps per episode (my `max_t = 2000`) to let each episode explore a bit more. Also, I updated `eps_decay` to be `0.9`, which is a little bit greedier than the default `0.995`, in order to attempt to prioritize experience a bit more over experimentation.

Using the default parameters resulted in significantly more episodes (around 500 - 800) to achieve the same 13 average reward.

### Improvements
Besides the obvious continued tweaking of hyperparameters, we could do the following to potentially make this network better:
1. Implement our QNetwork as a Double DQN. Although, while we might get better accuracy and learned behavior, we might pay a penalty, in terms of time to train. Therefore, it would be beneficial to back off on the amount of times between training.
2. Increase time between learning, in general. Potentially, just as in #1, tuning the amount of time we are training could be improved to do so a bit less often. Since our default `max_t` is 1000, we could easily try to learn every 100 steps or so.
3. Potentially, we could tweak the architecture of the QNetworks, by adding an additional hidden layer, or by adjusting hidden layers with decreasing numbers of nodes. As with each of these improvements, it just depends on your time and willingness to attempt each improvement.
