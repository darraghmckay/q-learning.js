qlearner.js
=============
--------------
Q-Learning Algorithm in JavaScript

It's based on this tutorial: [A Painless Q-Learning Tutorial](http://mnemstudio.org/path-finding-q-learning-tutorial.htm).

However this is a fork of the original Q-Learning Library written by [Nrox](https://github.com/nrox/q-learning.js).

It now supports an alpha parameter and is based off the following equation
[![Q-Learning Equations](https://upload.wikimedia.org/math/5/2/4/524fe99e01b50c2d0b3268cf418b6890.png)](#eqn)

Demo 
----------

[Chrome's T-Rex Game (QLearning)](https://darraghmckay.github.io/Learning-TRex)


Usage Example
==============

_____________________________



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


Running
-------
Calculate the Best Action for a given state, based off it's Qvales

    var ba = learner.bestAction(state);



This is all you need to successfully set up a q-learning system. 
It is a good idea to have it pick random Actions if a particular action isn't known for a given state, as follows:

    var random_action =      learner.actions[Math.floor(Math.random()*learner.actions.length)];
    
    //Pick the Best possible action (if there is any)
    action = learner.bestAction(current_state);
     
    //Decide, based on exploration settings, whether to try the random one or use the known one
    if (action===null || action === undefined || (!learner.knowsAction(current_state, random_action) && Math.random()< 0.2)){
               action = random_action;
     }
     
    //Set the Action
    current_action = Number(action);

Output
----
To Output the Qvalues (State / Action Pairs) in JSON

    JSON.stringify(learner.qvalues);



