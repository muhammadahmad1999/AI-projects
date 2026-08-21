## An illustrative example
### Problem statement
* $$\bold{p} = \begin{bmatrix}shape \\ texture \\ weight\end{bmatrix}$$
* Orange: $$\bold{p}_1 = \begin{bmatrix}1 \\ -1 \\ -1\end{bmatrix}$$
* Apple: $$\bold{p}_2 = \begin{bmatrix}1 \\ 1 \\ -1\end{bmatrix}$$

## Perceptron
* a single layer perceptron with a symmetric hard limit transfer function
### Two input case
* $$a = hardlims(n) = hardlims(\begin{bmatrix}-1 & 1\end{bmatrix}\bold{p} + b)$$
* if the inner product (dot product) of the weight matrix with the input vector is greater than or equal to $-b$, the output will be 1. If this is less than $-b$, the output will be -1.
* For the following line of points, the net input is equal to $0$:
$$n = \begin{bmatrix}-1 & 1\end{bmatrix}\bold{p} - 1 = 0$$
* The decision boundary will always be orthogonal to the weight matrix and the position of the boundary can be shifted by changing $b$.
* In general, $\bold{W}$ is a matrix consiting of a number of row vectors, and there will be a boundary for each row.
* the single neuron perceptron can separate input vectors into two categories - the decision boundary between the two categories is determined by the equation:
$$\bold{Wp} + b = 0$$
* because the boundary must be linear, the single layer perceptron can only be used to recognise patterns that are linearly separable - can be separated by a linear boundary.

## Pattern recognition example
* because there is only a two categories, we can use a single neuron
* as the inputs are three dimensional vectors ($R = 3$), the perceptron equation will be: $$a = hardlims(\begin{bmatrix}w_{1,1} & w_{1,2} & w_{1,3}\end{bmatrix} \begin{bmatrix}p_1 \\ p_2 \\ p_3\end{bmatrix} + b)$$
* we need to choose the weight matrix ($\bold{W}$) and bias ($b$) so that, for example, the perceptron outputs $1$ when an apple is input and $-1$ wwhen an orange is input
* from visually inspecting the problem (look in book for diagram), the boundary that separates the two prototype vectors is the $p_1, p_3$ plane
* the $p_1,p_3$ plane can be described through the equation $$p_2 = 0$$ or $$\begin{bmatrix}0 & 1 & 0\end{bmatrix} \begin{bmatrix} p_1 \\ p_2 \\ p_3 \end{bmatrix} + 0 = 0$$
* therefore the weight matrix and bias will be the following: $$\bold{W} = \begin{bmatrix} 0 & 1 & 0 \end{bmatrix}, b = 0$$
* the weight matrix is orthogonal to the decision boundary and points toward the region that contains the prototype pattern $\bold{p_2}$ (apple) for which we want the perceptron to produce an output of $1$.
* the bias is $0$ because the decision boundary passes through the origin
* Orange:
$$ a = hardlims(\begin{bmatrix} 0 & 1 & 0 \end{bmatrix} \begin{bmatrix} 1 \\ -1 \\ -1 \end{bmatrix} + 0) = -1$$
* Apple:
$$ a = hardlims(\begin{bmatrix} 0 & 1 & 0 \end{bmatrix} \begin{bmatrix} 1 \\ 1 \\ -1 \end{bmatrix} + 0) = 1$$
* what happens if we put in a not so perfect orange into the classifier - for example, an orange with an elliptical shape passes through the sensors - the input vector will be: $$\bold{p} = \begin{bmatrix} -1 \\ -1 \\ -1 \end{bmatrix}$$
the response of the network will be:
$$a = hardlims(\begin{bmatrix} 0 & 1 & 0 \end{bmatrix} \begin{bmatrix} -1 \\ -1 \\ -1 \end{bmatrix} + 0) = -1$$
which is classified as an orange
* in fact any input vector that is closer to the orange prototype vector than to the apple prototype vector (in Eucledian distance) will be classified as an orange and vice versa

### Hamming network
* explicitly designed to solve binary pattern recognition problems
* has both feedforward and recurrent (feedback) layers
* the number of neuron in the first layer is the same as the number of neurons in the second layer
* the objective of the Hamming network is to decide which prototype vector is closest to the input vector
* there is one neuron in the recurrent layer for each prototype pattern
* when the recurrent layer converges, there will be only one nueron with nonzero output
* this neuron indicated the prototype pattern that is closest to the input vector
* Feedforward layer:
$$\bold{a}^1 = \bold{purelin}(\bold{W}^1\bold{p} + \bold{b^1})$$
* Recurrent layer:
$$\bold{a}^2(0) = \bold{a}^1$$
$$\bold{a}^2(t + 1) = \bold{poslin}(\bold{W}^2\bold{a}^2(t))$$

### Feedforward layer
* the feedforward layer performs a correlation (or inner product) between each of the prototype patterns and the input pattern
* to do the above, the rows of the weight matrix in the feedforward layer are set to the prototype patterns. For our apple and orange example:
$$\bold{W}^1 = \begin{bmatrix} \bold{p}^T_1 \\ \bold{p}^T_2 \end{bmatrix} = \begin{bmatrix} 1 & -1 & -1 \\ 1 & 1 & -1 \end{bmatrix}$$
* each element of the bias vector is equal to $R$ (the number of elements in the input vector):
$$\bold{b}^1 = \begin{bmatrix} 3 \\ 3 \end{bmatrix}$$
* the output of the feedforward layer is:
$$\bold{a}^1 = \bold{W}^1\bold{p} + \bold{b}^1 = \begin{bmatrix} \bold{p}^T_1 \\ \bold{p}^T_2 \end{bmatrix} \bold{p} + \begin{bmatrix} 3 \\ 3 \end{bmatrix} = \begin{bmatrix} \bold{p}^T_1\bold{p} + 3 \\ \bold{p}^T_2\bold{p} + 3 \end{bmatrix}$$
* the output of the feedforward layer is equal to the inner products of each prototype pattern with the input plus $R$
* for two vectors of equal length (norm), their inner product will be largest when the vectors point in the same directons and will be smallest when they point in the opposite directions
* By adding $R$ to the inner product we guarantee that hte outputs can never be negative
* this is required for proper operation of the recurring layer
* the network is called Hamming network because the neuron in the feedforward layer with the largest output will correspond to the prototype pattern that is closest in Hamming distance to the input pattern

### Recurrent layer
* the recurrent layer is known as a competitive layer
* the neurons in the recurrent layer are initialised with the outputs of the feedforward layer, which indicated the correlation between the prototype patterns and the input vector
* then the neurons compete with each other to determine the winner
* after the competition, only one neuron will have a nonzero output
* the winning neuron indicated which category of input was presented to the network
* the $poslin$ transfer function is linear for positive values and zero for negative values
* the weight matrix $\bold{W}^2$ has the form:
$$\bold{W}^2 = \begin{bmatrix}1 & -\epsilon \\ -\epsilon & 1 \end{bmatrix}$$
* where $\epsilon$ is some number less than $1 / (S - 1)$ and $S$ is the number of neurons in the recurrent layer
* an iteration of the recurrent layer proceeds as follows:
$$\bold{a}^2(t + 1) = \bold{poslin}(\begin{bmatrix}1 & -\epsilon \\ -\epsilon & 1 \end{bmatrix} \bold{a}^2(t)) = \bold{poslin}(\begin{bmatrix}a^2_1(t) - \epsilon a_2^2(t) \\ a^2_2(t) - \epsilon a_1^2(t) \end{bmatrix})$$