#uni 
# Artificial Neural Network (ANN) architectures and Multilayer Perceptrons (MLPs)
ANNs gained popularity in the 1940s and 1980s.

# Artificial Neuron
Mathematical model of the biological neuron (simplified):
![[Pasted image 20260521150159.png]]
# Perceptron
A perceptron is composed of a single layer of units, where each unit is connected to all the inputs -- also called **fully connected or dense layer**:
![[Pasted image 20260521150318.png]]

# Activation Functions
## Logistic Function
## Hyperbolic Tangent Function
$$
\text{tanh}(x)=\frac{e^x-e^{-x}}{e^x+e^{-x}}
$$
Output between -1 and 1.
Continuous and derivable.
## Rectified Linear Unit Function:
$$
\text{ReLu}(x)=\max(0,x)
$$
continuous but not differentiable at x=0.
This is the default activation function.
# Modern MLP architecture for classification
![[Pasted image 20260521153230.png]]
# Learning Procedure
We need to find out how each connection weight and bias term should be optimized in order to reduce the error