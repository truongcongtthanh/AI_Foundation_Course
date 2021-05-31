# OPTIMIZER trong MACHINE LEARNING
https://viblo.asia/p/optimizer-hieu-sau-ve-cac-thuat-toan-toi-uu-gdsgdadam-Qbq5QQ9E5D8#
## 1. Gradient Descent (GD) - Giảm dần độ dóc
- Được sử dụng để tìm điểm tối ưu nhưng còn rất nhiều hạn chế
## 2. Stochastic Gradient Descent (SGD)
- Trong mỗi epoch, lấy ngẫu nhiên 1 điểm dữ liệu trong N điểm trong N lần để cập nhật N lần weighs và bias
- Nó sẽ chạy theo đường ziczac (lâu hơn)
![](https://i.imgur.com/YTSTviv.png)

```python=
def stochastic_gradient_descent():
    n_epochs = 50
    learning_rate = 0.01
    
    # khởi tạo giá trị tham số
    thetas = np.random.randn(2, 1)
    
    thetas_path = [thetas]
    losses = []
    
    for epoch in range(n_epochs):
        for i in range(m):
            # lấy ngẫu nhiên 1 sample
            random_index = np.random.randint(m)
            xi = X_b[random_index:random_index+1]
            yi = y[random_index:random_index+1]
            
            # tính output (o = x1*w1 + x2*w2)
            oi = xi.dot(thetas)
            
            # tính loss li [l = (output - y)^2]
            li = (oi - yi)*(oi - yi)
            
            # tính gradient cho loss
            g_li = 2*(oi - yi)
            
            # tính gradient (g_x1 = x1*g_li) và (g_x2 = x2*g_li)
            gradients = xi.T.dot(g_li)
                        
            # update giá trị theta
            thetas = thetas - learning_rate*gradients
            
            # logging
            thetas_path.append(thetas)            
            losses.append(li[0][0])
    return thetas_path, losses
bgd_thetas, losses = stochastic_gradient_descent()
plt.scatter(X, y)
data_y = X*bgd_thetas[-1][1]+ bgd_thetas[-1][0]
plt.plot(X,data_y, color="r")
plt.show()
```
### 2.1 Ưu điểm
- Giải quyết được dữ liệu lớn mà GD k làm được
- Sử dụng trong online learning 
### 2.2 Nhược
- Chưa giải quyết được learning_rate và parameter initialization (được giải quyết sau = **MOMENTUM** hoặc **AdaGrad..**)

## 3. MOMENTUM (theo đà tiến tới)
![](https://i.imgur.com/hQyBVy1.png)
![](https://i.imgur.com/GZLPzkO.png)
- Tuy chạy lâu hơn nhưng đạt được tới đúng điểm mong muốn

## 4. Adagrad
![](https://i.imgur.com/3hFrAVo.png)
- Ưu điểm:
    - Adagrad tránh việc điều chỉnh Learning rate bằng tay
    - Chỉ cần để tốc độ học default = 0.01 thì thuật toán sẽ tự động điều chỉnh
- Nhược:
    - tổng bình phương biến thiên sẽ lớn dần theo thời gian
    - Việc training sẽ khó khăn và trở nên đóng băng theo thời gian

## 5. RMSprop
- Chia cho trung bình của bình phương GD
![](https://i.imgur.com/gAuwpGM.png)

- Ưu: giải quyết được vấn đề tốc độ học giảm dần của Adagrad
- Nhược: có thể chỉ cho local minimum chứ k đạt được global minimum như Momentum

:arrow_right: Kết hợp RMSprop và Momentum sẽ cho ra thuật toán tối ưu
## 6. Adam
- Nếu Momentum như là 1 quả cầu lao dốc xuống thì Adam như là 1 quả cầu rất nặng lao xuống global minimum nhưng lại không dao động qua lại như Momentum
![](https://i.imgur.com/fi7emeO.png)

![](https://i.imgur.com/nRP5GrP.png)
