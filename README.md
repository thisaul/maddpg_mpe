DDPG_MPE

Tensorflow Implementation of the MADDPG algorithm from [*Multi-Agent Actor-Critic for Mixed
Cooperative-Competitive Environments*](https://arxiv.org/abs/1706.02275) (Lowe et. al. 2017)

## Requirements

* [Multiagent-Particle Environments (MPE)](https://github.com/openai/multiagent-particle-envs)
* dependencies: Python (3.5.4), OpenAI Gym (0.10.5), NumPy (1.14.5)

## Code structure

- `maddpg_mpe.ipynb`: core code for the MADDPG algorithm and different training scenarios in MPE

- `make_env.py`: contains code for importing a multiagent environment as an OpenAI Gym-like object

- `replay_buffer.py`: replay buffer code for MADDPG

- `distributions.py`: useful probability distributions

- `utils.py`: useful tensorflow functions

## Training parameters

- `MAX_EPISODE_LEN`: maximum length of each episode for the environment (default: `25`)

- `NUM_EPISODES`: total number of training episodes (default: `25000`)

- `LR`: learning rate (default: `1e-2`)

- `BATCH_SIZE`: batch size (default: `1024`)

- `NUM_UNITS`: number of units in the MLP (default: `64`)

## Training scenarios

| Name in paper | Env name | Notes |
| --- | --- | --- |
| Cooperative Communication | `simple_speaker_listener.py` | One agent is the ‘speaker’ (gray) that does not move (observes goal of other agent), and other agent is the listener (cannot speak, but must navigate to correct landmark).|
| Predator-Prey | `simple_tag.py` | Good agents (green) are faster and want to avoid being hit by adversaries (red). Adversaries are slower and want to hit good agents. Obstacles (large black circles) block the way. |
| Cooperative Navigation | `simple_spread.py` | N agents, N landmarks. Agents are rewarded based on how far any agent is from each landmark. Agents are penalized if they collide with other agents. So, agents have to learn to cover all the landmarks while avoiding collisions. |
| Physical Deception | `simple_adversary.py` | 1 adversary (red), N good agents (green), N landmarks (usually N=2). All agents observe position of landmarks and other agents. One landmark is the ‘target landmark’ (colored green). Good agents rewarded based on how close one of them is to the target landmark, but negatively rewarded if the adversary is close to target landmark. Adversary is rewarded based on how close it is to the target, but it doesn’t know which landmark is the target landmark. So good agents have to learn to ‘split up’ and cover all landmarks to deceive the adversary. |
