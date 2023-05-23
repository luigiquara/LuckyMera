<h1 style="text-align: center;">LuckyMera: a Modular AI Framework for Building Hybrid NetHack Agents</h1>

## Description

LuckyMera is an integrated framework built around the game of NetHack, one of the oldest and hardest roguelike video games.
The architecture is designed to build intelligent agents for the game, by constructing high-level game strategies.
LuckyMera is built following the principles of compositionality, modularity and extensibility; this means that the behavior of the agent is determined by a set of *skill* modules, that implement a series of actions to solve specific tasks.
It offers a high-level interface so that it is easy to define and integrate new modules.

LuckyMera leverages the challenging environment offered by NetHack to help AI researchers in designing, integrating and testing new approaches.
It is well-suited to try both symbolic modules and neural ones, giving also the possibility to experiment with hybrid solutions.

# ???
LuckyMera offers a symbolic agent, some neural modules, a way to save trajectories, a training mode with BehavioralCloning implemented.
# ???

## Installation

LuckyMera needs essentially ```nle``` to work properly.
# ???
Optionally, [```nle_language_wrapper```](https://github.com/Pervasive-AI-Lab/nle-language-wrapper) is needed to obtain text observation, and ```stable-baselines``` to use our implementation of the Behavioral Cloning algorithm.
# ???

After installing the dependencies, it can be installed by simply cloning the repository.
```
git clone https://github.com/Pervasive-AI-Lab/LuckyMera
```

## Getting started
LuckyMera can be configured via a simple ```config.json``` file and a handy *command-line* interface.

### ```config.json```
The configuration file is used to specify the parameters that influence the most the agent's behavior.

```
{"skill_priority_list": [
"Pray",
"Eat",
"Elbereth",
"Run",
"Break",
"Fight",
"Gold",
"StairsDescend",
"StairsAscend",
"ExploreClosest",
"Horizon",
"Unseen",
"HiddenRoom",
"HiddenCorridor"
],

"fast_mode": "on",
"attempts": "5"
}
```

You can change the skills' priority list, and with that you can define the play style of the agent, making it more brave or prudent.
Additionally, you can set whether to use the fast mode or not, and the number of games to play before terminating.

### *Command-line* interface

The *command-line* interface is used to set the runtime parameters of the architecture, and in particular to select the mode of use.
In fact, LuckyMera comes with three options:
+ *Inference* mode: use the framework agent, with the specified configuration, to play the game. You can also specify which observation the agent is allowed to use:
+ *Trajectory saving* mode: save the experiences of the agent in the form of *\<state-action\>* pairs. You have to specify the observation keys you want to save; using the option ```--language_mode```, you can select the text observation given by [```nle_language_wrapper```](https://github.com/Pervasive-AI-Lab/nle-language-wrapper):
+ *Training* mode: use the framework to train a neural model. You can specify the training algorithm and the dataset to use, together with other typical hyperparameters, *e.g.* the learning rate, the batch size and the number of epochs:

### Trying LuckyMera
```
# inference mode
$ python -m main 
       --inference
       --observation_keys glyphs chars

# trajectory saving mode
$ python -m main
       --create_dataset 
       --keys_to_save glyphs chars
       --filename path/to/dataset

# training mode
$ python -m main --training
       --training_alg BehavioralCloning
       --dataset path/to/dataset --learning_rate 1e-5
       --batch_size 32 --epochs 5
       --checkpoint path/to/model
```

# Cite LuckyMera

If you used LuckyMera in your work, please cite our wonderful paper!