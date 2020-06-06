---
title:  A Meta-MDP Approach to Exploration for Lifelong Reinforcement Learning (Garcia and Thomas)
date:   2020/06/06 15:04:11 +0700
tags: [RL, MetaLearning, NeurIPS2019]
---

# Introduction

I got aware of this paper at the NeurIPS 2019 conference in Vancouver. You can find the official paper <a href="https://arxiv.org/abs/1902.00843" target="_blank">here</a>. The source code is hosted in <a href="https://github.com/fmaxgarcia/Meta-MDP" target="_blank">this GitHub repo</a>.

In this paper, Garcia and Thomas consider two aspects of reinforcement learning: exploration and exploitation. Whereas traditional RL explores randomly and learns the exploitation policy, here they learn one extra policy for exploration. That extra policy is meta-learned from a distribution of tasks (simple variations of an MDP), so that it is possible to transfer it to new tasks (from the same distribution) to guide the agent more efficiently than random exploration. Why is this interesting? Because if we learn how to explore, then exploiting on other problems should be much faster. 

<!-- You could think about this as learning how to perform key actions that will reveal so that later the RL agent can focus on learning the particularities of the new environment (explotation policy). -->

Before going through the paper, I recommend checking reinforcement learning concepts and approaches. In particular, you might want to check how the Q-Learning, PPO, and REINFORCE algorithhms work. An additional aspect (not strictly necessary) is meta-learning for RL, specifically Model-Agnostic Meta-Learning (MAML).

# Background

## Reinforcement learning: exploration and exploitation

Reinforcement learning (RL) is an approach to automate goal-directed learning. It relies on two entities that interact with each other: an *environment* that delivers information of its *state*, and an *agent* that using such information learns how to achieve a *goal* in the environment. The interaction is a bilateral communication where the agent performs *actions* to modify the state of the environment, which responds with a numeric *reward* measuring how good the action was to achieve the goal. Typically, the sole interest of the agent is to improve its decision-making strategy, known as the *policy*, to maximize the total reward received over the whole interaction trial. The interaction runs for a number _T_ of time-steps, in which the agent improves its policy (a mathematical model) via a _learning rule_. The longer the interaction, the better the result (or at least that is the assumption). Figure 1 illustrates this process with the Atari's Breakout.

{% asset_img RL.png "Figure 1. An example of the reinforcement learning interaction between an agent and the environment." %}

<br/>
What distinguishes a specific RL algorithm from the others is (mainly) the model for the policy (e.g., a fully-connected neural network, an RNN, a lookup table, etc.) and the _learning rule_ used to improve it. On the contrary, a characterisct they all usually share is the notion of _exploration_ and _exploitation_, which are the focus of the paper we discuss here.

To understand _exploration_ and _exploitation_ intuitively, let's think of the Atari's Breakout. Imagine that you have never played a video game in your entire life and Breakout is your first one ever. In the beginning you will have to play several times to _explore_ the game: test the possible actions you can exectue with your remote controller, see the different ways of dying, finding rewarding sequences of actions (starting point of a strategy), etc. Once you learned that, you can focus on _exploiting_ that knowledge (improving the strategy) to get a better score (reward). Each RL algorithm defines its rules for this process. I would identify two main groups: the algorithms that explicitely set an schedule for exploration/exploitation (e.g. DQN) and the ones that do not. For the latter, I would not say that exploration is inexistent, but rather it is intrinsically associated to their learning rule (e.g., gradient descent _explores_ a "hill" until it settles in a local optimum). Garcia and Thomas focus on explicitely scheduled exploration.

That being said, exploration can have different interests. As Garcia and Thomas mention in their paper's introduction, exploration could focus on _when_ to explore, _how much_ exploration is neded, or (the question they try to answer) _what action to take at any exploration step_. The way I understand the latter is that an agent could learn what the most insightful actions are during exploration, which is different from the most rewarding ones (happening at exploitation time).

## Lifelong learning

Lifelong learning (for artificial intelligence) is a paradigm that aims to replicate in AI a specific behavior of human learning: we become more knowledgeable about a domain `T` with every learning experience related to it, and concurrently we improve our learning  strategy `L`. To understand this with an example, consider a neural network `nn` that should solve a set of tasks from domain `T`. From a programmatic point of view, lifelong learning could be seen as iterating over the tasks with a `nn.L(task)` function. Such a function should `return` some value `lifelong_info` that will be embedded into the network (e.g., calling `nn.improve(lifelong_info)`). Next time `nn` deals with a task of `T`, it will have a better strategy to learn and solve more efficiently and accurately.

If you want to learn more about Lifelong learning, surely you can find something useful <a href="https://www.cs.uic.edu/~liub/lifelong-learning.html" target="_blank">here</a>.

## Meta-Learning
Wikipedia's definition for meta-data is "data that provides information about other data". For those familiar with web development, the _headers_ in an HTTP request might help to understand. A header is indeed meta-data; i.e., additional information that is not essential to the core of HTTP communication but it could help a website to accomplish specific functionality. It could be anything and that is the main insight I want you to take.

<!-- Meta-learning (in machine learning) relies on meta-data, wh -->

<!-- For the purposes of this post it is convinient to introduce _meta-learning_ as a tool that can be used to achieve lifelong learning. I like to explain meta-learning by considering first what meta-data is.  -->

Meta-learning (in machine learning) relies on meta-data, which could be anything. It could be a plain timestamp of the OS, or the output of a very complex mathematical function. If you consider a task and a neural network `nn`, meta-data can be statistics from the dataset associated to the task, the value of a network's parameter at an specific iteration, the number of the iteration, an embedding at a given iteration, an aggregation of embeddings, and so on. Again, from a programmatic perspective, consider a database `DB` storing meta-data that `nn` can use and alter at any moment during the learning process `L`. Meta-learning can be seen as a function `nn.L(task, DB)`. If we are in a setting where multiple tasks are used, then `DB` is shared accross all tasks. Of course, the `DB` is just an abstraction, it could range from a simple variable changing its value within the algorithm to an RDBMS.

Meta-learning is a very interesting field with some very complex approaches. I encourage you to read <a href="https://arxiv.org/abs/1810.03548" target="_blank">this survey by J. Vanschoren</a> to take a closer look at this amazing field.

# The approach in a nutshell


# Understanding the key elements

# Experiments and results

# My feelings about the paper