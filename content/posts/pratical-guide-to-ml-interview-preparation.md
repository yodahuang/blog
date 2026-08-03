---
title: "Pratical Guide to ML Interview Preparation"
date: 2026-08-02T16:32:05-07:00
draft: false
---

The blog post is typed char-by-char by a real human™.

I tried my best so my blog does not contain anything work related. Then it would be a sad work blog. But I do need a place to host this piece. So it goes.

---

Some background. My day job is software engineer / research engineer / ml engineer / member of technical staff, whatever you call it. Basically, I train model and I also work on things related to the model: data / infra / eval. I have background in robotics and autonomous driving. 

Years ago when I was loooking for my first job things are relatively simple: 4 rounds of leetcoding, 1 round of "design this robot, what sensor would you choose, what algo would you use", and 1 round of "explain linear regression to me", and maybe a round for "lets' go over Kalman filter", since I worked on robots.

As I looked for new opportunities now things are different, for prepare for the interviews it seems you need to do your own BFS, or, more precisely, [IDDFS](https://en.wikipedia.org/wiki/Iterative_deepening_depth-first_search) for covering the topics. I hope my blog can give you an outline of what that looks like.

### Tensor programming

There are two types of tensor programming:
- Use `numpy` or `torch` or `jax`, given tensor input `x`, do operation `foo` and give output `y`.
  - E.g. L2 distance between two tensors
  - Ask your favorite LLM to generate test cases for you and you can practice it.
- Write out the vectorized version of an algorithm.
  - Typically you can write out the "normal" version, and then convert that to the vectorized version

I find it helpful to review ideas of broadcasting and advanced indexing. You need to get the dimensions really correct.

### Let's implement X

- Using primative operators, write out the forward / backward pass of common layer / functions
  - E.g. softmax, cross entropy loss, linear layer
- Write out forward for these more complex ones:
  - Multi-head attention
  - MoE layer
  - RoPE?
  - Flash Attn? (I cant do this)

### Do you know X

You can find a bunch of these questions online but I want to stress that you gonna really think about the real answer to these questions yourself, as I'm not satisfied with some "reference answer" out there.

E.g.
- Why are there the normalization term in attention? (Why is only attention have this strange term?)
- [Your domain-specific question here]
  - Sparse attention?
  - PPO/GRPO/DAPO?

So you gonna read about some big-name papers in the field. You can ask for big-name paper recommendation with your favorite chatbot LLM.

It's also a good idea to review some basic ideas you may have long forgotten:
- What exactly is [KL Divergence](https://notes.yanda.rocks/ML/KL-Divergence)? forward mode, backward mode, etc.
- What exactly is entropy?
- Reparameterization [trick](https://notes.yanda.rocks/ML/Reparameterization-trick)?
- How does [Adam](https://notes.yanda.rocks/ML/Adam) work?

### What if X

Here's the interesting part. I find the interviewers tend to ask things about what they are currently working on or would working on in the future. Knowing what they are currently working on is hard, but we can do a loose prediction here by consulting their previous experience.

Good sources are the their personal website and previously published papers. You can also go to LinkedIn and see if they've put something there. You can even talk to any LLM with web access: "I'm going to be interviewed by John Doe. Browse their online presense and see what they could be questioning me".

It's common case that you may not be able to find much information online. In that case, we should read all the recent tech blog of the company, taking their product in mind. I'm mostly preparing for robot companies. So the question in mind would be "if I were to implement this thing they demoed, how would I do it?". And LLM can be your critic. Do know that the LLMs have knowledge cutoff date, and I find the suggestion they have for me is too conservative. Feel free to push back.

### LLM

You gonna know the basics for LLM even if the target job does not really need you to work on LLMs. I think that's kinda reasonable, considering that's the area that got the most research. Previously the language modeling is copying ideas from computer vision. Now it's the other way around.

Things to consider:
- Write the full training loop of a GPT-2 like model with PyTorch / JAX.

### Other domain

Maybe transformer is not all you need:
- Diffusion / flow matching
- State space model (Mamba etc.)
- CNNs are still alive

Maybe supervised learning is not enough:
- Self supervised learning
  - Contrastive learning (CLIP etc.)
  - Self distillation (DINO etc.)
  - Reconstruction based (VAE, VQGAN, MAE etc.)
  - Masked prediction (BERT etc.)
- Reinforcement learning
  - The policy gradient path: REINFORCE, Actor-Critic, TRPO, PPO
  - Various on policy / off policy method
  - And model based / model free

For these I'll suggest generating a toy problem and try to write the full code. E.g. Using REINFORCE with advantage, or Q-learning for a classic [frozen lake](https://gymnasium.farama.org/environments/toy_text/frozen_lake/) environment.

### Resources I find useful

I like courses

- [Neural Networks: Zero to Hero](https://karpathy.ai/zero-to-hero.html) by Andrej Karpathy
- [CS336: Language Modeling from Scratch](https://cs336.stanford.edu/) by Stanford, Tatsu Hashimoto and Percy Liang
  - I think homeworks are valuable, at least do HW1 all by yourself
- [CS285: Deep Reinforcement Learning](https://rail.eecs.berkeley.edu/deeprlcourse/) by Berkeley, Sergey Levine
- [MIT Course 6.S184: Generative AI with Stochastic Differential Equations](https://diffusion.csail.mit.edu/2026/index.html) or Introduction to Flow Matching and Diffusion Models, by MIT, Peter Holderrieth and Ezra Erives
