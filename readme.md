class: center, middle

## Artificial Intelligence

# Machine Learning for Games

<br>

Gerard Escudero & Samir Kanaan, 2019

<br>

![:scale 50%](figures/inverse.png)

.footnote[Source: [inverse](https://www.inverse.com/article/31467-artificial-intelligence-computer-human-game) ]

---
class: left, middle, inverse

# Outline

* .cyan[Introduction]

* Machine Learning

* Deep Learning

* Reinforcement Learning

* Unity ML-Agents Toolkit

* Genetic Algorithms

* References

---

# Classification Data Example

.center[
class      | sepal <br> length | sepal <br> width | petal <br> length | petal <br> width 
:--------- | -----: | ----: | -----: | ----: 
setosa     | 5.1    | 3.5   | 1.4    | 0.2   
setosa     | 4.9    | 3.0   | 1.4    | 0.2   
versicolor | 6.1    | 2.9   | 4.7    | 1.4   
versicolor | 5.6    | 2.9   | 3.6    | 1.3    
virginica  | 7.6    | 3.0   | 6.6    | 2.1    
virginica  | 4.9    | 2.5   | 4.5    | 1.7   
150 rows or examples (50 per class).red[*] 
]

* The .blue[class] or .blue[target] column is usually refered as vector .blue[_Y_] 

* The matrix of the rest of columns (.blue[attributes] or .blue[features]) is usually referred
as matrix .blue[_X_]

.footnote[.red[*] _Source_ : _Iris_ problem UCI repository (Frank &amp; Asunción, 2010)]

---

# Main objective

.large[Build from data a .blue[model] able to give a prediction to new .blue[unseen] examples.]

.center[![model](figures/model.png)]

where:
* _data = previous table_
* _unseen = [4.9, 3.1, 1.5, 0.1]_
* _prediction = "setosa"_

---

# Regression Data Example

.center[
quality | density | pH   | sulphates | alcohol
------- | ------- | ---- | --------- | -------
6       | 0.998   | 3.16 | 0.58      | 9.8
4       | 0.9948  | 3.51 | 0.43      | 11.4
8       | 0.9973  | 3.35 | 0.86      | 12.8
3       | 0.9994  | 3.16 | 0.63      | 8.4
7       | 0.99514 | 3.44 | 0.68      | 10.55
1599 examples & 12 columns (11 attributes + 1 target).red[*]
]

The main diference between classification and regression is the _Y_ or target values:

* .blue[Classification]: discrete or nominal values <br>
Example: _Iris_, {“setosa”, “virginica”, “versicolor”}.

* .blue[Regression]: continuous or real values <br>
Example: _WineQuality_, values from 0 to 10.

.footnote[.red[*] _Source_ : _wine quality_ problem from UCI repository (Frank &amp; Asunción, 2010)]
 
---

# Example method: 

#### kNN with k=1

* How can be give a prediction to next examples?

.center[
| class | sep-len | sep-wid | pet-len | pet-wid |
|:------|:--------|:--------|:--------|:--------|
| ??    | 4.9     | 3.1     | 1.5     | 0.1     |
Unseen classification example on _Iris_]

.center[
| target | density | pH   | sulphates | alcohol |
|:-------|:--------|:-----|:----------|:--------|
| ??     | 0.99546 | 3.29 | 0.54      | 10.1    |
Unseen regression example on _WineQuality_]

* Let’s begin with a representation of the problems...

---

# Classification Data Example

![:scale 90%](figures/knn.png)

---

# Regression Data Example

![:scale 90%](figures/knnR.png)

---

# 1 Nearest Neighbors algorithm

* classification & regression

$$h(T)=y_i$$

.center[where $i = argmin_i(distance(X_i,T))$, $n=\vert features\vert$]
.center[and $distance(X,Z) = \sqrt{(x_1-z_1)^2+\ldots+(x_n-z_n)^2}$]

* Classification example (Iris):
  - distances: [0.47, 0.17, 3.66, 2.53, 6.11, 3.45]
  - prediction = setosa (0.17)

* Regression example (WineQuality):
  - distances: [0.33, 1.32, 2.72, 1.71, 0.49] 
  - prediction = 6 (0.33)

--

* .blue[lazy learning]: it means that the kNN does nothing in learning step
  - it calculates all in classify step

* This can produce some problems real time applications
  - such as .blue[Games]

---

# How about games?

#### Application examples:

- .blue[Classification]: decision about braking a car.

| Brake? | Distance | Speed |
|-------:|---------:|------:|
| Y      | 2.4      | 11.3  |
| Y      | 3.2      | 70.2  |
| N      | 75.7     | 72.7  |
| N      | 2.8      | 15.2  |
| %?     | 79.2     | 12.1  |
.center[Source: (Millington, 2019)]

- .blue[Regression]: required amount of force in a curve.

---

# Decision Learning

- A basic application is learning .blue[decisions] from .blue[observations]

  - _decisions_ will become _classes_ ($Y$)

  - _observations_ will become _features_ ($X$)

- Some kind of measure is needed to evaluate the model
 
- .blue[The Balance of Effort]

  - Many times is harder learning than human dessign (such as Behaviour Tree)

---

# Some categories

#### When?

- .blue[Online]: learn as playing

- .blue[Offline]: 
  - learn from saved matches
  - .blue[bootstrapping]: AI component playing among them <br>
    Same algorithm with diferent paramenters <br>
    Diferent algorithms <br>
    ([See chess example](https://arxiv.org/pdf/1509.01549v2.pdf))

#### What?

- .blue[Intra-Behaviour]: atomic behaviour 
  - Example: previous examples of braking or curves

- .blue[Inter-Behaviour]: learns Decision Taking layer
  - Example: [SC2LE(StarCraft II Learning Environment)](https://arxiv.org/abs/1708.04782)

---

# Action Prediction

- It is a simple technique that tries to guess player movements from previous recordings

- Human behaviour is not random

- It is also called RPS from: rock-paper-scissor game

- Example for a simple RPS:
  - Movement: Left, Right
  - Recording: "LRRLRLLL"

- It requires a window size
  - Example: previous 3 movements

- It can produce unbeatable AIs
  - Some level adjustment would be needed

---
class: left, middle, inverse

# Outline

* .brown[Introduction]

* .cyan[Machine Learning]

* Deep Learning

* Reinforcement Learning

* Unity ML-Agents Toolkit

* Genetic Algorithms

* References

---

# Maximum likelihood estimation

| class      | cap-shape | cap-color | gill-size | gill-color |
|:-----------|:----------|:----------|:----------|:-----------|
| poisonous  | convex    | brown     | narrow    | black      |
| edible     | convex    | yellow    | broad     | black      |
| edible     | bell      | white     | broad     | brown      |
| poisonous  | convex    | white     | narrow    | brown      |
| edible     | convex    | yellow    | broad     | brown      |
| edible     | bell      | white     | broad     | brown      |
| poisonous  | convex    | white     | narrow    | pink       |
.center[up to 8 124 examples & 22 attributes .red[*]]


- What is $P(poisonous)$?

$$P(poisonous)=\frac{N(poisonous)}{N}=\frac{3}{7}\approx 0.429$$

.footnote[.red[*]  _Source_ : _Mushroom_ problem from UCI repository (Frank &amp; Asunción, 2010)]

---

# Naïve Bayes

#### Learning Model

$$\text{model}=[P(y)\simeq\frac{N(y)}{N},P(x_i|y)\simeq\frac{N(x_i|y)}{N(y)};\forall y \forall x_i]$$

.col5050[
.col1[
| $y$       | $P(y)$ |
|:----------|-------:|
| poisonous | 0.429  |
| edible    | 0.571  |
]
.col2[
| attr:value       | poisonous | edible |
|:-----------------|----------:|-------:|
| cap-shape:convex | 1         | 0.5    |
| cap-shape:bell   | 0         | 0.5    |
| cap-color:brown  | 0.33      | 0      |
| cap-color:yellow | 0         | 0.5    |
| cap-color:white  | 0.67      | 0.5    |
| gill-size:narrow | 1         | 0      |
| gill-size:broad  | 0         | 1      |
| gill-color:black | 0.33      | 0.25   |
| gill-color:brown | 0.33      | 0.75   |
| gill-color:pink  | 0.33      | 0      |
]
]

---

# Naïve Bayes

#### Classification

$$h(T) \approx argmax_y P(y)\cdot P(t_1|y)\cdot\ldots\cdot P(t_n|y)$$

- Test example $T$:

| class | cap-shape | cap-color | gill-size | gill-color |
|:------|:----------|:----------|:----------|:-----------|
| ??    | convex    | brown     | narrow    | black      |

- Numbers:
$$P(poisonous|T) = 0.429 \cdot 1 \cdot 0.33 \cdot 1 \cdot 0.33 = 0.047$$
$$P(edible|T) = 0.571 \cdot 0.5 \cdot 0 \cdot 0 \cdot 0.25 = 0$$
- Prediction: $$h(T) = poisonous$$

---

# Naïve Bayes

#### Notes

- It needs a smoothing technique to avoid zero counts <br>
  - Example: Laplace
$$P(x_i|y)\approx\frac{N(x_i|y)+1}{N(y)+N}$$

- It is empiricaly a decent classifier but a bad estimator
  - This means that $P(y|T)$ is not a good probability 

#### Implementation

- Using LINQ of C#: [view](codes/naiveBayes.html).red[*] / [output](codes/modelNB.txt) / [download code](codes/naiveBayes.cs)

.footnote[.red[*] Formated with http://hilite.me/]

---

# Gaussian Naïve Bayes

* How about numerical features?

| Brake? | Distance | Speed |
|-------:|---------:|------:|
| Y      | 2.4      | 11.3  |
| Y      | 3.2      | 70.2  |
| N      | 75.7     | 72.7  |
| N      | 2.8      | 15.2  |
| %?     | 79.2     | 12.1  |
.center[Source: (Millington, 2019)]

$$P(x_i|y)=\frac{1}{\sqrt{2\pi\sigma_y^2}}\exp\left(-\frac{(x_i-\mu_y)^2}{2\sigma_y^2}\right)$$

.center[where $\mu_y=\frac{x_1^y+\cdots+x_n^y}{n_y}$ and $\sigma_y^2=\frac{(x_1^y - \mu_y)^2+\cdots+(x_n^y - \mu_y)^2}{n_y-1}$]


---

# Gaussian Naïve Bayes

.col5050[
.col1[
**Learning model:**

| $y$  | $P(y)$ |
|:-----|-------:|
| Y    | 0.5    |
| N    | 0.5    |

<br>

|                 | Distance | Speed     |
|:----------------|---------:|----------:|
| $\mu_Y$         | 2.8      | 40.75     |
| $\mu_N$         | 39.25    | 43.95     |
| $\sigma_Y^2$    | 0.32     | 1734.605  |
| $\sigma_N^2$    | 2657.205 | 1653.125  |
]
.col2[
**Classification:**

$$P(Y|T)=0.5\cdot 0.0\cdot 0.00669 = 0.0$$

$$P(N|T)=0.5\cdot 0.00573\cdot 0.00722 = 0.00002$$

$$h(T)=N$$

**Note:**

$$P(speed=12.1|Y)=\frac{1}{\sqrt{2\cdot\pi\cdot 1734.605}}\cdot$$

$$\cdot \exp\left(-\frac{(12.1-40.75)^2}{2\cdot 1734.605}\right)=0.00669$$
]]

---

# Decision Trees

**Splitting measure:**

- Decision Trees: $accuracy=\frac{N(ok)}{N}$

- ID3: $entropy=-\sum_{\forall y} P(y) \cdot log_2(P(y))$

- CART: $gini = 1 - \sum_{\forall y} P(y)^2$ + binary trees

- .blue[Our approach]: $gini$ + k-ary trees

  - nominal and numeric features

  - classification and regression

  - one of the easiest decision trees

---

# Example I

.cols5050[
.col1[
| class      | cap-shape | cap-color |
|:-----------|:----------|:----------|
| poisonous  | convex    | brown     |
| edible     | convex    | yellow    |
| edible     | bell      | white     |
| poisonous  | convex    | white     |
| edible     | convex    | yellow    |
| edible     | bell      | white     |
| poisonous  | convex    | white     |
]
.col2[
**algorithm:**

each node of the tree from 

the minimum weighted sum of

 _Gini index_:

.small[$gini = 1 - \sum_{\forall y} P(y)^2$]
]]

---

# Example II

**cap-shape:**

| cap-shape | poisonous | edible | #examples |
|----------:|----------:|-------:|----------:|
| convex    | 3         | 2      | 5         |
| bell      | 0         | 2      | 2         |

.small[
.blue[For each _value_:]

$gini(\text{cap-shape}=\text{convex})=1-(\frac{3}{5})^2-(\frac{2}{5})^2=0.48$

$gini(\text{cap-shape}=\text{bell})=1-(\frac{0}{2})^2-(\frac{2}{2})^2=0.0$

.blue[_Weighted sum_:]

$gini(\text{cap-shape})=\frac{5}{7}\cdot 0.48+\frac{2}{7}\cdot 0.0=0.343$
]

---

# Example III

**cap-color:**

| cap-color | poisonous | edible | #examples |
|----------:|----------:|-------:|----------:|
| brown     | 1         | 0      | 1         |
| yellow    | 0         | 2      | 2         |
| white     | 2         | 2      | 4         |

.small[
.blue[For each _value_:]

$gini(\text{cap-color}=\text{brown})=1-(\frac{1}{1})^2-(\frac{0}{1})^2=0.0$

$gini(\text{cap-color}=\text{yellow})=1-(\frac{0}{2})^2-(\frac{2}{2})^2=0.0$

$gini(\text{cap-color}=\text{white})=1-(\frac{2}{4})^2-(\frac{2}{4})^2=0.5$

.blue[_Weighted sum_:]

$gini(\text{cap-color})=\frac{1}{7}\cdot 0.0+\frac{2}{7}\cdot 0.0+\frac{4}{7}\cdot 0.5=0.286$
]

---

# Example IV

**Selecting best feature:**

- best feature will be that with minimum _gini index_:

.small[
$$\text{best_feature}=\min((0.343,\text{cap-shape}),(0.286,\text{cap-color}))=\text{cap-color}$$
]

- every value with only a class will be a _leaf_:
  - brown $\rightarrow$ poisonous
  - yellow $\rightarrow$ edible

- a new set is built for the rest of values

.center[
| class      | cap-shape |
|:-----------|:----------|
| edible     | bell      |
| poisonous  | convex    |
| edible     | bell      |
| poisonous  | convex    |
_white_ examples without _cap-color_
]

- the process restarts with the new set

---

# Example V

**Resulting Tree:**

.center[
![:scale 75%](figures/dt.png)
]


---

# Cutting Points I

**What about numerical attributes?**

| class      | width |
|:-----------|------:|
| versicolor | 2.9   |
| versicolor | 2.9   |
| virginica  | 3.0   |
| virginica  | 2.5   |

**Cutting points:**

| class      | width | cutting points | weighted ginis |
|:-----------|------:|---------------:|:---------------|
| virginica  | 2.5   |      |   | 
| versicolor | 2.9   | 2.7  | $\frac{1}{4}\cdot 0.0+\frac{3}{4}\cdot 0.45=0.0.3375$ |
| versicolor | 2.9   |      |   |
| virginica  | 3.0   | 2.95 | $\frac{3}{4}\cdot 0.45+\frac{1}{4}\cdot 0.0=0.0.3375$ |
.center[.small[cutting points for _width_ attribute]]

---

# Cutting Points II

**Gini example:**

| width | versicolor | virginica | #examples | gini |
|:------|-----------:|----------:|----------:|:-----|
| < 2.7 | 0 | 1 | 1 | $1-(\frac{0}{1})^2-(\frac{1}{1})^2=0$ |
| > 2.7 | 2 | 1 | 3 | $1-(\frac{2}{3})^2-(\frac{1}{3})^2=0.45$ |

**Resulting Tree:**

.center[
![:scale 50%](figures/dt-ct.png)
]

---

# Regression


---
class: left, middle, inverse

# Outline

* .brown[Introduction]

* .brown[Machine Learning]

* .cyan[Deep Learning]

* Reinforcement Learning

* Unity ML-Agents Toolkit

* Genetic Algorithms

* References

---

# Artificial Neuron Model

.center[![:scale 55%](figures/neuron.png)]

.center[![:scale 60%](figures/neuron_model.png)]

.footnote[Source: [Artificial Neuron](http://www.gabormelli.com/RKB/Artificial_Neuron)]

---

# Perceptron

.cols5050[
.col1[

- Classification and regression

- Linear model

- Classification:

$$h(x)=f(\sum_{i=1}^n w_i x_i + b)$$

- Learning rule:

$$w_i'=w_i+\eta(h(x)-y)$$
]
.col2[

![:scale 100%](figures/hyperplane.png)

]]

- Example in sklearn:
  - [view](codes/nn-sklearn.html) / [download](codes/nn-sklearn.ipynb) / [reference](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Perceptron.html)

---

# Multi-layer Perceptron

.col5050[
.col1[- One hidden layer

- Non-linear model

- Classification & regression

- [Backpropagation](https://en.wikipedia.org/wiki/Backpropagation) as training algorithm

- Example in sklearn:
  - [view](codes/nn-sklearn.html) / [download](codes/nn-sklearn.ipynb) / [reference](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPClassifier.html#sklearn.neural_network.MLPClassifier)

- Main parameters:
  - hidden_layer_sizes
  - activation
  - max_iter

]
.col2[
![:scale 110%](figures/mlp.png)
]]

.footnote[Source: [wikipedia](https://en.wikipedia.org/wiki/Artificial_neural_network)]

---

# Bias, Variance & Overfitting

![](figures/bias.png)![](figures/early-stopping.png)

Normal use of a validation set to select parameters & avoid overfitting (to much learning)!

.footnote[Source: [left](https://towardsdatascience.com/regularization-the-path-to-bias-variance-trade-off-b7a7088b4577), [right](https://elitedatascience.com/overfitting-in-machine-learning)]

---

# Deep Learning

- Neural network with 2 or more hidden layers

![](figures/chart-1.png)

.cols5050[
.col1[
![](figures/chart-2.png)
]
.col1[
**Examples:**

- Sklearn on Iris
  - [view](codes/nn-sklearn.html) / [download](codes/nn-sklearn.ipynb)

- Keras on MNIST
  - [view](codes/keras-mlp.html) / [download](codes/keras-mlp.ipynb) / [Source](https://github.com/keras-team/keras)
]
]

.footnote[Source: [The Neural Network Zoo](https://www.asimovinstitute.org/neural-network-zoo/)]

---

# Convolutional Neural Networks

**from Computer Vision**

to process image & video

![:scale 90%](figures/cnn2.png)

.footnote[Source: [A Comprehensive Guide to Convolutional Neural Networks](https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53)]

---

# Convolutional Neural Networks II

.cols5050[
.col1[
- Convolution: extract the high-level features such as edges

- Pooling: reduce dimensionality for 
  - computational cost
  - extracting dominant features which are rotational and positional invariant

- Example:
  - Keras on MNIST
  - [view](codes/keras-cnn.html) / [download](codes/keras-cnn.ipynb) / [Source](https://github.com/keras-team/keras)
]
.col2[
![:scale 70%](figures/convolutional.gif)

![:scale 80%](figures/pooling.gif)
]]

.footnote[Source: [A Comprehensive Guide to Convolutional Neural Networks](https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53)]

---

# The Neural Network Zoo

![:scale 90%](figures/zoo-1.png)

.footnote[Source: [The Neural Network Zoo](https://www.asimovinstitute.org/neural-network-zoo/)]

---

# The Neural Network Zoo II

![:scale 90%](figures/zoo-2.png)

.footnote[Source: [The Neural Network Zoo](https://www.asimovinstitute.org/neural-network-zoo/)]

---

# The Neural Network Zoo III

![:scale 90%](figures/zoo-3.png)

.footnote[Source: [The Neural Network Zoo](https://www.asimovinstitute.org/neural-network-zoo/)]

---
class: left, middle, inverse

# Outline

* .brown[Introduction]

* .brown[Machine Learning]

* .brown[Deep Learning]

* .cyan[Reinforcement Learning]

* Unity ML-Agents Toolkit

* Genetic Algorithms

* References

---

# Reinforcement Learning

![:scale 65%](figures/rl.png)

.cols5050[
.col1[
- an _agent_
- a set of states $S$
- a set of actions $A$

]
.col2[
Learning a reward function $Q: S \times A \to \mathbb{R}$ for maximizing the total future reward.

]]

- _Q-Learning_: method for learning an aproximation of $Q$.

.footnote[Source: [My Journey Into Deep Q-Learning with Keras and Gym](https://medium.com/@gtnjuvin/my-journey-into-deep-q-learning-with-keras-and-gym-3e779cc12762)]

---

# Reinforcement Learning II

Training example:

.center[![:scale 55%](figures/q-matrix.png)]

.footnote[Source: [Reinforcement Q-Learning from Scratch in Python with OpenAI Gym](https://www.learndatasci.com/tutorials/reinforcement-q-learning-scratch-python-openai-gym/)]

---

# Deep Reinforcement Learning

- Convolutional Neural Network for learning $Q$ <br>

.center[[![:scale 65%](figures/breakout.png)](https://www.youtube.com/watch?v=TmPfTpjtdgg&feature=youtu.be)]

.footnote[Source: [Deep Reinforcement Learning](https://deepmind.com/blog/article/deep-reinforcement-learning)]

---
class: left, middle, inverse

# Outline

* .brown[Introduction]

* .brown[Machine Learning]

* .brown[Deep Learning]

* .brown[Reinforcement Learning]

* .cyan[Unity ML-Agents Toolkit]

* Genetic Algorithms

* References

---

# ML-Agents

Unity plugin for training intelligent agents.

[![:scale 70%](figures/mlagents.png)](https://www.youtube.com/watch?v=Hg3nmYD3DjQ&feature=youtu.be)

Address: https://github.com/Unity-Technologies/ml-agents

Contain .blue[Deep Learning] & .blue[Reinforcement Learning]

---
class: left, middle, inverse

# Outline

* .brown[Introduction]

* .brown[Machine Learning]

* .brown[Deep Learning]

* .brown[Reinforcement Learning]

* .brown[Unity ML-Agents Toolkit]

* .cyan[Genetic Algorithms]

* References

---

https://github.com/Sebastian-Schuchmann/Genetic-Algorithm-in-Unity3D

https://medium.com/@venkateshtata9/an-introduction-to-evolutionary-algorithms-and-code-part-1-theory-behind-genetic-algorithm-df75af08d5d6

https://bitbucket.org/kryzarel/generic-genetic-algorithm/src/master/
https://forum.unity.com/threads/tutorial-genetic-algorithm-c.479062/

https://github.com/jonasstr/Genetic-Algorithm-TSP-Unity


- Ús: ajust de paràmetres i de nivells

---

# Parameter Modification

- We have lots of magic numbers in our AI so far, remember steering ?

- How we could have a process to automatically generate the best setup ?

- We could train offline the AI in different setup and evaluate the results

- First we need a fitness value: a heuristic on how well it performs

-  E.g. we randomly setup the vectors and have the AI go from A to B
  - Fitness value could be time to target, distance taken, damage from collisions, etc.

- We can have the game run several hundreds of time

- This produce some statistics ...

- We try to not go fully random but improve the search with inform decisions

- We use a technique called hill climbing: we keep exploring what looks like the
best fitness / lower energy

2 gràfiques

---
class: left, middle, inverse

# Outline

* .brown[Introduction]

* .brown[Machine Learning]

* .brown[Deep Learning]

* .brown[Reinforcement Learning]

* .brown[Unity ML-Agents Toolkit]

* .brown[Genetic Algorithms]

* .cyan[References]

---

# References

- Ian Millington. _AI for Games_ (3rd edition). CRC Press, 2019.

- Gerard Escudero. [_Supervised Machine Learning_](https://gebakx.github.io/classification/slides/machineLearning.pdf). 2019. 

- Sefik Ilkin Serengil. [_A Step by Step CART Decision Tree Example_](https://sefiks.com/2018/08/27/a-step-by-step-cart-decision-tree-example/). 2018. It also contains a regression example.

- Llibre i/o documentació de ML-Agents.

- Article DeepMind.

- Hands on machine learning.

- Keras.

- Algorismes genètics.

