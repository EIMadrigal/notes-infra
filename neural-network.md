# Neural Network

input layer: $$x$$ is a column vector

$$
a^{(0)} = x
$$

hidden layer:

$$
z^{(l)} = W^{(l)} a^{(l-1)} + b^{(l)}
$$

$$
a^{(l)} = \sigma (z^{(l)})
$$

output layer:

$$
\hat {y} = \phi (W^{(L)} a^{(L-1)} + b^{(L)})
$$

Backpropagation

output layer:

$$
\frac{\partial L}{\partial W^{(L)}}=\frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial z^{(L)}} \cdot \frac{\partial z^{(L)}}{\partial W^{(L)}}=(\hat{y} - y) \cdot \sigma^{'}(z^{(L)})\cdot a^{(l-1)}
$$

the error item describes the gradient regarding to $$\frac{\partial L}{\partial z^{(L)}}$$

$$
\delta^{(L)} = (\hat{y} - y) \odot \sigma^{'}(z^{(L)})
$$

$$
\frac{\partial L}{\partial b^{(L)}}=\frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial z^{(L)}} \cdot \frac{\partial z^{(L)}}{\partial b^{(L)}}=(\hat{y} - y) \cdot \sigma^{'}(z^{(L)})=\delta^{(L)}
$$

hidden layer:

$$
\frac{\partial L}{\partial W^{(l)}}=\frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial z^{(l)}} \cdot \frac{\partial z^{(l)}}{\partial W^{(l)}}=\delta^{(l)} \cdot a^{(l-1)}
$$

the error item:

$$
\delta^{(l)} = \frac{\partial L}{\partial z^{(l)}}=\frac{\partial L}{\partial z^{(l+1)}}\cdot \frac{\partial z^{(l+1)}}{\partial z^{(l)}}=\delta^{(l+1)}\cdot W^{(l+1)}\cdot \sigma^{'}(z^{(l)})
$$

$$
\frac{\partial L}{\partial b^{(l)}}=\delta^{(l)}
$$

Gradient update:

$$
W^{(l)}=W^{(l)}-\eta \frac{\partial L}{\partial W^{(l)}}
$$

$$
b^{(l)}=b^{(l)}-\eta \frac{\partial L}{\partial b^{(l)}}
$$

