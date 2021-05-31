# Một số ứng dụng trong AI
### 1. Bài toán trích xuất thuộc tính bằng đạo hàm
![](https://i.imgur.com/jmcPI2O.png)
![](https://i.imgur.com/ku30Jrp.png)

### 2. Bài toán Zoom hình bằng nearest_neighbor và linear regression: 
![](https://i.imgur.com/SBaJmPs.png)
![](https://i.imgur.com/iWNiFGB.png)
![](https://i.imgur.com/MuxTZJe.png)

### 3. Đổi background 
![](https://i.imgur.com/MSLBhYR.png)

- Mask là gì??
![](https://i.imgur.com/VWYkHH5.png)

- Phép trừ background
![](https://i.imgur.com/Slr2CqF.png)

### 4. Xoá nhiễu cho background
![](https://i.imgur.com/f9K54Xi.png)

- Bằng cách dùng phép nhân ma trận
![](https://i.imgur.com/gK0a5H2.png)

- Công thức tính hình chiếu
![](https://i.imgur.com/3olkirY.png)

### 5. Tính Cosine
- Sử dụng nhân từng phần tử ma trận với nhau
![](https://i.imgur.com/1TND1Ew.png)
![](https://i.imgur.com/z6VJXH5.png)

### 6. bài toán Stereo matching: Đo khoảng cách tới các object trong hình, tracking, detect..
- Matching từng điểm
![](https://i.imgur.com/UoSIteP.png)
![](https://i.imgur.com/ifJ0ARH.png)

- Matching từng windown
![](https://i.imgur.com/TKLXTlq.png)
![](https://i.imgur.com/MB3Lc5W.png)

- Kết quả phụ thuộc nhiều vào độ sáng
![](https://i.imgur.com/6mzA262.png)
![](https://i.imgur.com/a8rvI9n.jpg)

- Stereo matching: dùng Cosine similarity và tích phân cho tốc độ kết quả khác nhau
![](https://i.imgur.com/X8QF9SX.png)

- Cách tính diện tích với tích phân: áp dụng chung cho 2 chiều
![](https://i.imgur.com/VOo7P8p.png)

- Cách tính mới: tính ra 1 list F(lớn) tương đương
![](https://i.imgur.com/YnHx713.png)

- Tính theo công thức chuẩn rời rạc:
![](https://i.imgur.com/iv3PBuC.png)

- Sử dụng Mean:
![](https://i.imgur.com/r1FtViG.png)


### 7. Ứng dụng làm mờ ảnh, khuôn mặt...
![](https://i.imgur.com/Kdud0j5.png)

- Source code: dùng hàm filter2D, để tính correlation theo kernel
![](https://i.imgur.com/ZQDBlHk.png)
![](https://i.imgur.com/v1SEKbd.png)

- Output sẽ giảm kích thước sau khi correlation với kernel 
![](https://i.imgur.com/htt8nQS.png)
![](https://i.imgur.com/eFR4LMg.png)

- Để làm mờ khuôn mặt, ta phải nhận diện, rồi làm mờ khuôn mặt, sau đó gián khuôn mặt đã làm mờ lên khuôn mặt trong hình gốc
![](https://i.imgur.com/fLHm69X.png)

### 8. Khử nhiễu:
- Dùng Median: hàm medianBlur
![](https://i.imgur.com/GEDA3oW.png)
![](https://i.imgur.com/u3JxIGT.png)

- Median (Trung vị): số ở giữa (hoặc trung bình 2 số ở giữa) của dãy đã được sắp xếp
![](https://i.imgur.com/7uXEvdf.png)
![](https://i.imgur.com/eWHDywb.png)

 
### 9. Điều chỉnh độ sáng ảnh với Histogram
![](https://i.imgur.com/ophCTEg.png)
![](https://i.imgur.com/OZZRHZn.png)
![](https://i.imgur.com/M4UG69T.png)

- Để có một bức ảnh được phối độ sáng hợp lý ta có thể điều chỉnh phân bố hợp lý
![](https://i.imgur.com/TZ2FMID.png)
![](https://i.imgur.com/5i1WND6.png)

- Công thức phân bố lại độ sáng:
![](https://i.imgur.com/K6M2waR.png)
![](https://i.imgur.com/yCTcZFL.png)

### 10. Tìm texture của một hình bằng Variance (Phương sai)
![](https://i.imgur.com/6pMQ6KA.png)

- Công thức tìm phương sai:
![](https://i.imgur.com/JLCYI6E.png)
![](https://i.imgur.com/5FPhfPE.png)

- Cách thức hoạt động
![](https://i.imgur.com/jsRVXvs.png)

- Cách thực hiện: tính theo từng window, dùng adaptive window để lấy size phù hợp
![](https://i.imgur.com/8hBqAmx.png)

- Đồ thị mình hoạ theo window
![](https://i.imgur.com/BJ3an7E.png)

- Source code:
![](https://i.imgur.com/Q1ewDs3.png)

### 11. Tìm template có sẳn trong hình
![](https://i.imgur.com/zx0WfJO.png)

- Sử dụng correlation coefficient (Hệ số tương quan - Mối tương quan giữa 2 biến (x tăng -> y thế nào (tăng hay giảm bao nhiêu lần)))
- Với tính chất 2: chịu được sự thay đổi của ánh sáng khi detect object
![](https://i.imgur.com/GCg3rse.png)

- Source code
![](https://i.imgur.com/vartswt.png)

- Ứng dụng trong việc so sánh tương quan giữa 2 ảnh
![](https://i.imgur.com/Jxz7KLB.png)

- Detect object
![](https://i.imgur.com/SZwHq4p.png)

### 12. Bài toán tìm đường đi
- Sử dụng genetic alogrithm
![](https://i.imgur.com/cH3eULx.png)

- Bài toán sức chứa tối đa
![](https://i.imgur.com/CTHNVxQ.png)

- Bài toán định tuyến người giao hàng
- Giải thuật gen:
    - Đi qua từng bước để tạo quần thể mới 
![](https://i.imgur.com/3qsaH63.png)
    - Sắp xếp lại quần thể theo độ tối ưu tăng dần
    - Giữ lại m gen con cao nhất, còn lại tiếp tục lai tạo để được trạng thái tối ưu hơn
- Các bước và source code:
    - Tạo quần thể ngẫu nhiên
    ![](https://i.imgur.com/KznYucp.png)
    - Tính quan các gen của quần thể
    ![](https://i.imgur.com/k6IVw4I.png)
    - Lựa chọn các gen để lại tạo (random)
    ![](https://i.imgur.com/Q6HrRNa.png)
    ![](https://i.imgur.com/HptXBnn.png)
    ![](https://i.imgur.com/V4cZF0W.png)
    - Lai tạo
    ![](https://i.imgur.com/hpc899B.png)
    - Đột biến
    ![](https://i.imgur.com/lzBdHpO.png)
- Ứng dụng trong bài toán tìm hàm tối ưu
![](https://i.imgur.com/xYKy9gJ.png)
![](https://i.imgur.com/WwkO1V3.png)
![](https://i.imgur.com/ovVRYam.png)

### 13. Bài toán Linear Regression (Hội quy tuyến tính)
- Bài toán:
![](https://i.imgur.com/ZkPvSHt.png)
![](https://i.imgur.com/YmFeSNj.png)

- Tính toán ban đầu
![](https://i.imgur.com/5L4b1g4.png)

- Ví dụ mẫu: 
![](https://i.imgur.com/N73Tya1.png)
- Tính toán lại giá trị w, b => thu được loss giảm
![](https://i.imgur.com/AS2xOxr.png)
- Kết quả ta có được là:
![](https://i.imgur.com/Up4VgIU.png)

- Đồ thị các bước làm:
- Có 10 dòng dữ liệu, ta sẽ train từng dòng 1. Khi train đủ 10 dòng ta nói train được 1 epoch
- 1 epoch có thể là 1 phần của data set
![](https://i.imgur.com/zKOiQJN.png)
    
- Bình thường người ta chỉ train từng dòng với 1 phần data
![](https://i.imgur.com/sMxOPFn.png)

- Source code
```python=
# random space
import matplotlib.pyplot as plt
import numpy as np
import matplotlib.animation as animation
from IPython.display import HTML
from matplotlib.colors import LogNorm
from itertools import cycle
from numpy import genfromtxt
import numpy as np
from numpy import genfromtxt
import matplotlib.pyplot as plt

data = genfromtxt('data.csv', delimiter=',')
areas  = data[:,0]
prices = data[:,1]

data = genfromtxt('data.csv', delimiter=',')
m = 4
X = data[:,0]
y = data[:,1]
X_b = np.c_[np.ones((m, 1)), X]

eta = 0.01
index = 0
thetas = np.array([[0.04],[-0.34]])

losses = []

def compute_gradient(index):
    global thetas
    global losses
    
    xi = X_b[index:index+1]
    yi = y[index:index+1]
    
    oi = xi.dot(thetas)
    li = (oi - yi)*(oi - yi)
    
    losses.append(li[0][0])
    #print(xi, yi)
    #print('\n loss: ', li)
    
    g_li = 2*(oi - yi)
    gradients = xi.T.dot(g_li)
    
    thetas = thetas - eta*gradients
    
    a = thetas[1][0]
    b = thetas[0][0]
    
    return a,b

def update_plot(i): 
    plt.cla()
    
    global index
    global thetas
    
    index = index+1
    index = index%m
    #print(index)
    
    a,b = compute_gradient(index)
    #print(a,b)
    
    plt.scatter(areas, prices)
    x_value = np.arange(3,8)

    y_value = a*x_value + b 
    plt.plot(x_value, y_value,c='red')

    plt.xlabel('Diện tích nhà (x 100$m^2$)')
    plt.ylabel('Giá nhà (chục lượng vàng)')
    
    plt.xlim(2,8)
    plt.ylim(3,10)

fig, ax = plt.subplots(figsize=(8, 5))
a,b = compute_gradient(index)

plt.scatter(areas, prices)
x_value = np.arange(3,8)

y_value = a*x_value + b 
plt.plot(x_value, y_value,c='red')

plt.xlabel('Diện tích nhà (x 100$m^2$)')
plt.ylabel('Giá nhà (chục lượng vàng)')

plt.xlim(2,8)
plt.ylim(3,10)

#plt.show()
ani = animation.FuncAnimation(fig, update_plot, interval=2000, frames=range(30), fargs=())    
#HTML(ani.to_html5_video())
ani.save('chap6_data_gif_2.gif', writer='imagemagick', fps=1)
```







