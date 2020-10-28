# Linear Regression
## 1. Machine learning
![](https://i.imgur.com/wh51FTO.png)

### 1.1 Supervised Learning
![](https://i.imgur.com/CajH4OX.png)

## 2. Derivative/Gradient
![](https://i.imgur.com/ChOrFub.png)

## 3. Linear Regression
![](https://i.imgur.com/GD2GxdX.png)
![](https://i.imgur.com/WkGuKCc.png)
![](https://i.imgur.com/GCveHwF.png)
![](https://i.imgur.com/jxGUtmU.png)
![](https://i.imgur.com/zFHlNVJ.png)
After many loop

## 4. Computational graph
![](https://i.imgur.com/C9mA4OR.png)
![](https://i.imgur.com/Ca8QvbU.png)
![](https://i.imgur.com/O0jM0nR.png)
![](https://i.imgur.com/HYGVVsJ.png)
![](https://i.imgur.com/HWqdgIk.png)
for 2 elements

![](https://i.imgur.com/V8KVYlC.png)
![](https://i.imgur.com/NIFJN6P.png)
for 4 elements

![](https://i.imgur.com/46ptnXj.png)
![](https://i.imgur.com/m1zpFK0.png)
Use Matrix

```python=
import numpy as np
from numpy import genfromtxt
import matplotlib.pyplot as plt

data = genfromtxt('data.csv', delimiter=',')

# X_b chứa thêm bias (=1)
m=4
X = data[:,0]
y = data[:,1:]
X_b = np.c_[np.ones((m, 1)), X]

n_epochs = 1
eta = 0.01
thetas = np.array([[0.04],[-0.34]])
#thetas = np.array([[0.26676], [1.179292]])
#thetas = np.array([[0.28539967], [1.3041778]])
print('thetas', thetas)

thetas_path = [thetas]
losses = []

for epoch in range(n_epochs):
    sum_of_losses = 0
    gradients = np.zeros((2,1))
    
    for index in range(2):
        xi = X_b[index:index+1]
        yi = y[index:index+1]
        
        print('\ndata: ', xi, yi)

        oi = xi.dot(thetas)
        li = (oi - yi)*(oi - yi)        
        g_li = 2*(oi - yi)
        
        print('\n\n z: ', oi)
        print('loss: ', index, li)
        print('gradient_loss: ', index, g_li)
        
        cg = xi.T.dot(g_li)
        print('variable gradient: ', index, cg)
        
        gradients = gradients + cg
        sum_of_losses = sum_of_losses + li
    
    sum_of_losses = sum_of_losses/2
    gradients     = gradients/2
    print('\ngradients: ', gradients)
    losses.append(sum_of_losses[0][0]) 
        
    thetas = thetas - eta*gradients
    print('new params: ', thetas)

```

<p align="right">Slide and source code from Dinh Quang Vinh teacher<p align="right">
