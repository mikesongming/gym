[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://pre-commit.com/) [![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

## Important Notice

### The team that has been maintaining Gym since 2021 has moved all future development to [Gymnasium](https://github.com/Farama-Foundation/Gymnasium), a drop in replacement for Gym (import gymnasium as gym), and Gym will not be receiving any future updates. Please switch over to Gymnasium as soon as you're able to do so. If you'd like to read more about the story behind this switch, please check out [this blog post](https://farama.org/Announcing-The-Farama-Foundation).

## Gym

Gym is an open source Python library for developing and comparing reinforcement learning algorithms by providing a standard API to communicate between learning algorithms and environments, as well as a standard set of environments compliant with that API. Since its release, Gym's API has become the field standard for doing this.

Gym documentation website is at [https://www.gymlibrary.dev/](https://www.gymlibrary.dev/), and you can propose fixes and changes to it [here](https://github.com/Farama-Foundation/gym-docs).

Gym also has a discord server for development purposes that you can join here: https://discord.gg/nHg2JRN489

## Installation

First, create a new virtual environment (optional but highly recommended) using your preferred tool.

```
conda create -n gym python=3.9
conda activate gym
```

To install the base Gym library, use

```
python -m pip install 'git+https://github.com/mikesongming/gym.git#egg=gym[all]'
```

We support Python 3.9, 3.10 on macOS.

Modify `moviepy`'s code for `use_clip_fps_by_default` in `decorators.py:L128`:

```
    # names = func_code.co_varnames[1:]
    import inspect
    names = inspect.getfullargspec(f).args[1:]
```


## API

The Gym API's API models environments as simple Python `env` classes. Creating environment instances and interacting with them is very simple- here's an example using the "CartPole-v1" environment:

```python
import gym
env = gym.make("CartPole-v1")
observation, info = env.reset(seed=42)

for _ in range(1000):
    action = env.action_space.sample()
    observation, reward, terminated, truncated, info = env.step(action)

    if terminated or truncated:
        observation, info = env.reset()
env.close()
```

## Notable Related Libraries

Please note that this is an incomplete list, and just includes libraries that the maintainers most commonly point newcommers to when asked for recommendations.

* [CleanRL](https://github.com/vwxyzjn/cleanrl) is a learning library based on the Gym API. It is designed to cater to newer people in the field and provides very good reference implementations.
* [Tianshou](https://github.com/thu-ml/tianshou) is a learning library that's geared towards very experienced users and is design to allow for ease in complex algorithm modifications.
* [RLlib](https://docs.ray.io/en/latest/rllib/index.html) is a learning library that allows for distributed training and inferencing and supports an extraordinarily large number of features throughout the reinforcement learning space.
* [PettingZoo](https://github.com/Farama-Foundation/PettingZoo) is like Gym, but for environments with multiple agents.

## Environment Versioning

Gym keeps strict versioning for reproducibility reasons. All environments end in a suffix like "\_v0".  When changes are made to environments that might impact learning results, the number is increased by one to prevent potential confusion.

## MuJoCo Environments

The latest "\_v4" and future versions of the MuJoCo environments will no longer depend on `mujoco-py`. Instead `mujoco` will be the required dependency for future gym MuJoCo environment versions. **Old gym MuJoCo environment versions that depend on `mujoco-py` are REMOVED**.
To install the dependencies for the latest gym MuJoCo environments use `pip install gym[mujoco]`.

## Citation

A whitepaper from when Gym just came out is available https://arxiv.org/pdf/1606.01540, and can be cited with the following bibtex entry:

```
@misc{1606.01540,
  Author = {Greg Brockman and Vicki Cheung and Ludwig Pettersson and Jonas Schneider and John Schulman and Jie Tang and Wojciech Zaremba},
  Title = {OpenAI Gym},
  Year = {2016},
  Eprint = {arXiv:1606.01540},
}
```

## Release Notes

There used to be release notes for all the new Gym versions here. New release notes are being moved to [releases page](https://github.com/openai/gym/releases) on GitHub, like most other libraries do. Old notes can be viewed [here](https://github.com/openai/gym/blob/31be35ecd460f670f0c4b653a14c9996b7facc6c/README.rst).
