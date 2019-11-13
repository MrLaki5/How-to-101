
## Rng terms:

* flatten layers - transforms multy dimensional input to 1d output

* dense layers - fully connected layers (every two neurons from two layers are connected)

* softmax function - function that takes array of k elements and returns array consisting of k probabilities.

* relu activation function - function that returns 0 for all negative input, and linear maping from x to y on positiv input. Other similar functions that are worse in performance are: tanh, sigmoid.

## CNN (convolutional neural networks):

* Deep neural networks used in computer vision with specific layer. First layer, convolutional layer, is layer which takes input featchures. But instead of taking pixel by pixel it takes matrixes of pixels that are near each other and applys to them some filter that can provide some attributes to show clearely (etc. edges, blureness...). This featchures give neural network option to detect edges.

* Stride - number of pixels that frame will move for calculating each featchure matrix. 

* Padding - when filters do not align with image you can eather add zeros or crop some part of image.

* Pooling - layers that reduce number of parameters when images are too large.

* Relu (Rectified Linear Unit) - function that convers negative input to 0 and leaves positive input. Used to convert all negative values pixels at start.

* FC - Fully connected layer, deep neural network layer.

* Architecture of CNN looks like: input => (X) convolution + relu => pooling => If more "cropping" needed go to (X); else continue; => flatten => FC => softmax => output


## Optimizers:

### Optimizers are algorithms that provide how will weights be changed in training of model.

* *SGD* (Stochastic Gradient Descent) - algorithm that is used for finding minimum of function with derivative of function and looking at its slope. (Closer to minimum, slope is closer to 0). Every weight has same learning rate (value that is multiplied in formula for weight changing when minimum of function has not been found).

* *RMSprop* (Root Mean Square Propagation) - algorithm that has specific learning rate for all weights. All learning rates are adapted based on the average of their recent amplitudes.

* *Adagrad* (Adaptive Gradient Algorithm) - algorithm that has specific learning rate for all weights. All learning rates are adapted based on how frequently a weight is updated during training. More updated, smaller learning rate.

* *Adadelta* - more robust extension of Adagrad that adapts learning rates based on moving window of gradient updates instead of accumulating all past gradients. This way adadelta continues to learn after meny updates are done.

* *Adam* (Adaptive Moment Estimation) - instead of adapting learning rates based on the everage first momentum (mean in RMSprop), adam also makes use of the average of the second momentum of the gradients. Algorithm calculates squared gradient (like other algorithams) and exponential moving average of the gradient for second momentum. And parameters beta1 and beta2 control decay rates of this momentums.

* *Adamax* - variant of Adam based on infinity norm.

* *Nadam* - its Adam algorithm with Nesterov momentum.


## Loss functions:

### Loss functions are used in training of model. Goal of training is to minimize output of this functions.

* *mean_squared_error* - (1/N) * sum((Y1 - Y2)^2)

* *mean_absolute_error* - (1/N) * sum(abs(Y1 - Y2))

* *mean_absolute_percentage_error* - (1/N) * sum(abs((Y1 - Y)/Y1))

* *mean_squared_logarithmic_error* - (1/N) * sum(log(Y1 + 1) - log(Y2 + 1))

* *hinge loss function* - Used for training classifiers, "maximum-margin" classification in SVM (support vector machine). Maximum margin means that algorithm is searching for largest margin that can be put in dataset to devide classes.
