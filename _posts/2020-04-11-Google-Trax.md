---

title: "Considering Google's Trax for Deep Learning "
date: 2020-04-11T16:49:53+00:00
categories:
  - blog
  - deep-learning
tags:
  - ramble
  - sources
  - cross-posted
  - google
---


# Google's Trax

Intended audience: software engineers, machine learning engineers, aspiring deep learning researchers (warning: it's a small niche)

Epistemic status: "cold take" distillation, as I've been exploring the codebase in off-hours and coffee breaks for months

# Introduction

[The Trax library](https://github.com/google/trax) works to be an easy ramp onto deep learning:

![top lines of the project READ ME](/assets/images/2020-04-11-Google-Trax/header.png)

Other notes:

- They have [the implementation of the Re-former](https://github.com/google/trax/tree/master/trax/models/reformer) (an efficient, modified [Transformer network](https://arxiv.org/abs/1706.03762)) in the codebase

## Instructions/explanation is in the *code*.

This will bring comfort to some. Many software engineers that want to get down and dirty with machine learning and these sexy "neural networks" they here about in the news. But where to begin? Grok [the code](https://github.com/google/trax/tree/master/trax).

---

This is honestly not my preference. I've been a software engineer for five years and getting thrown into a new codebase has never been my favorite part of the job. It's not terrible, but I don't relish in that space; my more of a "greenfield guy". I might have had more funny working with the team that produced the Trax codebase than the team that is currently maintaining it. If that's the same group, I would be *stunned,* given the size of Google, but I digress.

---

The [quick start tutorial](https://colab.research.google.com/github/google/trax/blob/master/trax/intro.ipynb) shows you just where to jump in and play, with slight hints as to what to avoid. It's already wired up, so it's really up to you to figure out how to plug and play:

- See which hyperparameters have a significant impact on training
- See what kind of problems you can model for the Transformer language model can learn.
- It's easier than ever to dig into [a codebase with Colab](https://colab.research.google.com/notebooks/intro.ipynb), as they've implemented Ctrl/Cmd + LeftClick and a file browser. If they keep this up, I won't have a reason to use Jupyter notebooks anymore

The model you'll train is not perfect. Far from it, even. Just supply a negative number and watch the predictions go nuts.

Enough critiquing, the tutorial code is well organize and serves as a jumping-off point to start learning. That's what tutorials are supposed to do: get you going.

Google's instruction also gives us a nice example of well-formatted logging.

## A gold-mine of clean code

Searching around Trax, you will find a legitimate implementation of [the Re-former architecture](https://github.com/google/trax/tree/master/trax/models/reformer), [implementations of Attention from first-principles](https://github.com/google/trax/blob/master/trax/layers/attention.py), and an awesome [decorator that dynamically generates Python classes to serve as Layer implementations](https://github.com/google/trax/blob/8a399915368a27d10728d8504c592337a2fb1bd3/trax/layers/base.py#L567). That's just the start. The code is tremendously well organized by SOLID architecture principles.

- Things that change for the same reasons live together. Guess where the introduction to [the Trax Layers API lives](https://github.com/google/trax/blob/master/trax/layers/intro.ipynb)?
- Implementations are concise, making it hard to get lost in the sauce. A great example is `[layers/rnn.py](https://github.com/google/trax/blob/master/trax/layers/rnn.py)`, which actually pointed me to [a paper](https://arxiv.org/abs/1709.02755) that I *hadn't heard about* in the NLP/NLU space: [Simple Recurrent Units](https://github.com/google/trax/blob/master/trax/layers/rnn.py#L244)
- Implementations look much more like the math that is happening that typical Python/Numpy/Tensorflow tends to look
- The goal of the codebase is to be expressive and easy to learn from. Just look at this [implementation of BERT](https://github.com/google/trax/blob/master/trax/models/research/bert.py)
- There are [unit tests aplenty](https://github.com/google/trax/blob/master/trax/layers/base_test.py), living right next to the code it tests.

Just a quick note: a lot of the completed implementations seem oriented around language modeling, rather than computer vision (CV) stuff. If you want CV tutorials, Tensorflow prime has you covered. I've been looking for more legible NLP code, so this is a huge win for me.

# Conclusion

In spending time reading the code, I've gotten a feel for how [Google Brain](https://research.google/teams/brain/) (who has been tremendously successful in pushing ML forward) thinks about their work; I've found some great, yet concise, papers that have pushed sub-fields forward; and I've seen a new perspective on how to write code for someone else to read. (Maybe I'll write about that next.)

If Trax turns out to be of use to you, that would be great. If it's the one resource you needed that, 8 months from now you're starting at Google AI, maybe remember who helped you out 😄 If you're not impressed with the codebase and NLP isn't your thing, I appreciate you reading this far.

Till then.
