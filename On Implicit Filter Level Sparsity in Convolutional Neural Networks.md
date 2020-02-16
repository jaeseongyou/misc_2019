# On Implicit Filter Level Sparsity in Convolutional Neural Networks



## Findings

* **Regularization** induces higher sparsity than **no regularization**
  * No regularization, no sparsity
  * Sparsity positively correlated with regularization strength
* **L2 regularization** induces higher sparsity than **weight decay regularization**

* **Adaptive variants** induce higher sparsity and selectivity than **SGD**
* **Easier task**, **smaller network**, **smaller batch size** induce higher sparsity



## BasicNet

![model2](/home/jsy/Projects/Study/dl/gangnam/images/model2.png)

![model](/home/jsy/Projects/Study/dl/gangnam/images/model.png)



## Weight Decay vs L2 Regularization 

#### Aren't they the same?

* Deep Learning, p224 (Goodfellow, Bengio, Courville)

  "...*the L2 parameter norm penalty commonly known as weight decay*" 

* Point made

  L2 regularizer interacts with the update mechanism (more direct influence on the gradients)

  Weight Decay does NOT (less influence on the gradients)

  


#### L2 regularization

"$\lambda \theta$ is added to the gradient $\nabla L(\theta)$ from the main objective, and the update step is computed using this sum."

$\theta_{t+1} = \theta_{t} - \alpha (\nabla L(\theta_{t}) + \lambda \theta_{t})$

i.e.   $\theta_{t+1} = \theta_{t} - \alpha \nabla L(\theta_{t}) - \alpha \lambda \theta_{t}$



#### Weight decay

"multiplies theta by $(1-\lambda)$ after the update step based on the gradient from the main objective"

$\theta_{t+1} = \theta_{t} - \alpha \nabla L(\theta_{t})$

$\theta_{t+1} = (1-\lambda)\theta_{t+1}$

i.e. 	$\theta_{t+1} = \theta_{t} - \alpha (1-\lambda) \Delta L(\theta_{t}) - \lambda \theta_{t}$



## Quantifying Feature Sparsity

#### Per-Feature Activation 

​	Apply max pooling to the absolute activations over the entire feature map for each filter

​	Inactive if $ < 10^{-12}$ over the entire training corpus



#### Per-Feature Scale

​	gamma of the learned BN layer where $y_{i} = \gamma \hat{x_{i}} + \beta$

​	Inactive if $|\gamma| < 10^{-3}$



## Quantifying Feature Selectivity

#### Selectivity

​	Apply max pooling to the absolute activations over the entire feature map for each filter

​	Normalize by the max of the pooled activations over the entire training corpus

​	Get the percentage of training corpus that cannot activate a feature over $10^{-3}$ 

​	*universality = 1 - selectivity



## Usages

More control on sparsity of a network

​	bypass the explicit sparsification/pruning 

​	preserve the generalization performance



## Table 1

![table1](/home/jsy/Projects/Study/dl/gangnam/images/table1.png)

* Adaptive optimizers generate higher sparsity
* Stronger regulation generate higher sparsity
* Easier task generates higher sparsity
* In case of Adam, L2 induces higher sparsity than weight decay



## Table 2

![table2](/home/jsy/Projects/Study/dl/gangnam/images/table2.png)

* Higher sparsity in the earlier layers

* L2-Adam generate more selective features in the later layers



## Tables Again

![table 3-6](/home/jsy/Projects/Study/dl/gangnam/images/table 3-6.png)

* Table 3~5: **a smaller batch size** leads to higher sparsity 
* Table 6: **smaller network capacity** leads to higher sparsity



## And Yet Again

![table 7-9](/home/jsy/Projects/Study/dl/gangnam/images/table 7-9.png)

* Comparison with explicit pruning: higher sparsity for comparable test performance 



## Figure 2

![Figure 2](/home/jsy/Projects/Study/dl/gangnam/images/Figure 2.png)

* Sparsity and variance of $\gamma$ and $\beta$ of batch norm layer is correlated.



## Figure 3

![Figure 3](/home/jsy/Projects/Study/dl/gangnam/images/Figure 3.png)

* Later layers tend to have more selective features
* Adam tends to have more selective features then SGD



## Figure 4

![Figure 4](/home/jsy/Projects/Study/dl/gangnam/images/Figure 4.png)

* L2-ADAM yields faster decay than WD-ADAM or L2-SGD

