## Introduction
Neuron output is calculated through: $$a = f(wp + b)$$

The actual output depends on the transfer function (activation function). The weights correspond to the strengths of the synapses in the dendrites, the body is represented by the summation operator and the output represents the axon - the activation function/transfer function controls whether an axon/output is fired or not and passed on to the next layer neuron or not.

## Transfer functions
Can be a linear or non-linear function of $n$ (neuron summation output).

Three of the most common transfer functions:
* Hard limit transfer function: sets the output of the neuron to $0$ if the function argument is less than $0$ or $1$ if its arguments is greater than or equal to $0$. The value $-b/w$ on the $x$-axis represents where the hardlim function transitions from $0$ to $1$ as the output: $$a = hardlim(n)$$ 
* Linear trasnfer function: the output is equal to its input. The value $-b/w$ on the $x$-axis represents where the purelin function intercepts the $x$-axis. $b$ represents the $y$-intercept: $$a = n$$
* Log-sigmoid transfer function: takes input and squashes the output into the range $0$ to $1$, according to the expression: $$a = \frac{1}{1 + e^{-n}}$$

## Multiple input neuron
* The calculation of a neuron with multiple inputs can be described in the following way using matrices and vectors: $$n = \bold{W}\bold{p} + b$$ where $\bold{W}$ is a matrix of weights and $\bold{p}$ is a vector of inputs
* The matrix $\bold{W}$ for a single neuron only has one row
* The neuron output can be written as $$a = f(\bold{W}\bold{p}+b)$$
* For the elements of the weight matrix, the first index indicates the particular neuron destination for that weight while the second index indicate the source of the signal that was fed to the neuron.
* For example, the indices in $w_{1,2}$ mean that this weight represents the connection to the first and only neuron from the second element (source) in the input vector.
* the input vector $\bold{p}$ has dimensions $R \times 1$ while for the single neuron example the weight matrix $\bold{W}$ has dimensions $1 \times R$.