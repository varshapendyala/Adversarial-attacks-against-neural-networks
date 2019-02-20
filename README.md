# Adversarial Attacks against neural networks
In this project, I implement this paper [Towards Evaluating the Robustness
of Neural Networks.](https://arxiv.org/abs/1608.04644) Lp norm based attack algorithms are designed to generate adversarial inputs to the deep neural networks.

MINIST handwritten digits dataset is considered to demonstrate the attacks against a trained model.

In [MNIST_training.ipynb](), I use Tensorflow's Keras APIs to construct the feedforward network, train and evaluate.
Model training is done with 'categorical_crossentropy' loss and 'SGD' optimizer with 0.01 learning rate. The trained model is saved as [my_MNIST.h5](). The model accuracy on the MNIST test data is close to 99.2%


[L2_attack.ipynb]() has the tensorflow code to produce adversarial examples for a given test image that is closer in terms of L2 distance metric. This code loads the MNIST dataset and chooses a particular image to test the L2 attack convergence.

  * *Load_Model()* loads the trained network on MNIST dataset into *model*.
  * Using *model*, a computational graph is constructed to perform the objective function minimization. 
  * The graph, session, tensors can be accessed through *Construct_Graph_Objfn()* class as *AG*.
  * *AG.Initialize_vars()* initializes all the globalvariables except the *model*'s parameters
  * Gradience descent on the objective function is performed with various values of *AG.const* whose value is updated based on binary search.
  * *initial_const*, *upper_bound*, *lower_bound*, *bs_steps*, corresponds to the above binary search.
  * *iterations* defines the number of iterations of gradient descent for each value of *AG.const*.
  * *Test_image* is our input image to the alogorithm that finds an adversary close to this image with target label being *t_label*
  
  For the given test input, the algorithm can be observed to be converging by the decreasing value of *AG.const* with every binary search update. This can be seen from the print output for every 500 iterations.
