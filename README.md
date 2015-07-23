qlearner.js
=============

Q-Learning Algorithm in JavaScript

It's based on this tutorial: [A Painless Q-Learning Tutorial](http://mnemstudio.org/path-finding-q-learning-tutorial.htm).

However this is a fork of the original Q-Learning Library written by [Nrox](https://github.com/nrox/q-learning.js).

It now supports an alpha parameter and is based off the following equation
[![Q-Learning Equations](https://upload.wikimedia.org/math/5/2/4/524fe99e01b50c2d0b3268cf418b6890.png)](#eqn)

Demo
-----

#[Example 1: basic](http://nrox.github.io/q-learning.js/test1.html)

#[Example 2: game agent](http://nrox.github.io/q-learning.js/test2.html)


Usage Example
=======

Learning
------

There are three arguments to the constructor
    Gamma, alpha, actions
    The default values for Gamma and Alpha are 0.8
    Actions is an array of possible actions (more can be added dynamically too)

    var learner = new QLearner(0.2,0.4,[1,2,3,4,5]);


Add transitions like this:

     learner.add(fromState, toState, reward, actionName);

In this last expression, if fromState or toState do not exist they are added automatically. If no reward is know pass
*undefined*, if actionName is not important leave it undefined.

If no reward is known and actionName is not important:

    learner.add(fromState, toState);

Reward is known and actionName is not important:

    learner.add(fromState, toState, reward);

Reward is not known and actionName is important

    learner.add(fromState, toState, undefined, actionName);

States and actions set, then make it learn. The argument is the number of iterations.

    learner.learn(1000);

Running
-------

To use what the learner *knows*. Set an initial state

    learner.setState('s0');

then call to choose the best action and automatically apply it.

    learner.runOnce();

and get the next state with

    var cur = learner.getState();

or get the best action:

    var ba = learner.bestAction();

or run it until it stays in the same state, or solution.

    var current = null;
    while (current!==learner.getState()){
        current = learner.getState();
        learner.runOnce();
    }


