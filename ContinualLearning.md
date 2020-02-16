# Continual Learning in Deep Learning Network by Using a Kalman Optimiser



Catastrophic forgetting



Ensemble learning

PathNet (dual-memory-based learning)

Gradient Episodic Memory (a subset of the samples)

Regularization-based method

Elastic Weight Consolidation





Karman Filter estimating Online Stochastic Natural Gradient Descent 





## Key

Let different parts of the parameters adapt to different tasks

(1) Obtain the important parameters in the previously learned tasks via Fisher Information matrix

(2) Group them in long-term memory units

(3) Group others in short-term memory units

(4) Parameters involved in each of the units are dynamically chosen at the end of each training process within a single nn layers.



## Methodology

### Gradient as an Uncertainty Measure

track the changes (uncertainty) of the weights and adjust them



## Kalman Optimizer

Restrict the changes of the weights to let the new value have lower uncertainty by using a Kalman Filter



At the end of the first training

​	prior knowledge: the uncertainty and the optimal solution of the first task

​	i.e.   initial info theta0 (the set of parameters in the pretrained model) 

​			uncertainty of model on the previous data P0

second training

​	track the changes in the weights and the uncertainty  



While training on the new dataset or for a new task, according
to the gradient descent process and mini-batch algorithm,
at batch k, we can predict the value ˆθk|k−1 and obtain an
uncertainty measure Rk which refers to the gradient of the
parameter θk−1 on the kth batch data.

The predicted values of the Kalman Filter would be close to the values that will result in lower uncertainty. 



## Questions

what is exactly the uncertainty? How is it defined?

multi-head approach?

How would you implement this?

We update the normalised Fisher Information recursively?

## Equations

$\hat{\theta}_{k|k-1} = \theta_{k-1} - \alpha * Gradients$ ()

$K_k = P_{k-1} / (P_{k-1} + R_{k} + \xi)$ 			(K: The Kalman Gain, R: uncertainty of theta_k-1 on the kth batch)

$\hat{\theta}_{k} = \theta_{k-1} + K_k(\hat{\theta}_{k|k-1} - \theta_{k-1})$		(P: The uncertainty of model)

$P_k = (I - K_k)P_{k-1}$

​		$P_k < P_{k-1}$

$F(\theta) = E_{\theta}[]$