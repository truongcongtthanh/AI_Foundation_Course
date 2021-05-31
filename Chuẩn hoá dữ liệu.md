# Chuẩn hoá dữ liệu
## 1. Dữ liệu cơ bản
![](https://i.imgur.com/UE3UQzo.png)

=> Làm cho species thành dạng số được phân loại

``` python=
# aivietnam.ai
# Đọc file IRIS.csv
import numpy as np
import numpy.core.defchararray as np_f
# lấy các đặc trưng và lưu vào biến X
X = np.genfromtxt('IRIS.csv', delimiter=',', dtype='float', usecols=[0,1,2,3], skip_header=1)
print(X.shape)
# lấy species và lưu vào biến y
y = np.genfromtxt('IRIS.csv', delimiter=',', dtype='str', usecols=4, skip_header=1)
# thay chuỗi bằng số
categories = np.unique(y)
for i in range(categories.size):
    y = np_f.replace(y, categories[i], str(i))    
# đưa về kiểu float    
y = y.astype('float')
print(y)
```

- Ở đoạn code trên:
    - dữ liệu số cần dùng được đưa vào X
    - Dữ liệu nhãn phân loại được chuẩn hoá về dạng số
    
- Ta có kết quả trả về như sau:
![](https://i.imgur.com/O1hqEp0.png)

- Download data = code, 
    - tuple(0): link cần down
    - tuple(1): nơi cần để lưu
![](https://i.imgur.com/SbrdUlY.png)

## 2. DỮ liệu dạng binary - MNIST dataset
- Đọc và Xử lý file .gzip 
- Source code lấy 60000 tập train và 10000 tập test
``` python=
import os
import gzip
import numpy as np
def load_fashion_mnist(path, kind='train'):    
    """Load fashion_MNIST data from `path`"""
    labels_path = os.path.join(path, '%s-labels-idx1-ubyte.gz' % kind)
    images_path = os.path.join(path, '%s-images-idx3-ubyte.gz' % kind)
    with gzip.open(labels_path, 'rb') as lbpath:
        labels = np.frombuffer(lbpath.read(), dtype=np.uint8, offset=8)
    with gzip.open(images_path, 'rb') as imgpath:
        images = np.frombuffer(imgpath.read(), dtype=np.uint8, offset=16).reshape(len(labels), 784)
    return images, labels
X_train, y_train = load_fashion_mnist('data_fashion_mnist/')
print(X_train.shape)
print(y_train.shape)
X_test, y_test = load_fashion_mnist('data_fashion_mnist/', kind='t10k')
print(X_test.shape)
print(y_test.shape)
```
- Bỏ 8 byte đầu tiên của tập **LABEL** chứa thông tin mô tả về file
- Bỏ 16 byte đầu tiền của tập **TRAIN**
- Data lưu ở dạng vector 784 thay cho 28x28 = 784

``` python=
import matplotlib.pyplot as plt 
import numpy as np 
# Tạo dang sách 100 phần tử ngẫu nhiên từ X_train có 60.000 phần tử
indices = list(np.random.randint(X_train.shape[0],size=100))
fig =plt.figure(figsize=(9,9))
columns = 10
rows = 10
for i in range(1, columns*rows +1):
    img = X_train[indices[i-1]].reshape(28,28)
    fig.add_subplot(rows, columns, i)
    plt.axis('off')
    plt.imshow(img, cmap='gray', vmin=0, vmax=255)
plt.show()
```
- Source code để display 100 hình dữ liệu 1 cách random, ta có result
![](https://i.imgur.com/x9QcfJr.png)

### Source code lấy 50000 tập train và 10000 tập test và 10000 tập validate

``` python=
import os
import gzip
import numpy as np
def load_fashion_mnist(path, kind='train'):    
    """Load fashion_MNIST data from `path`"""
    labels_path = os.path.join(path, '%s-labels-idx1-ubyte.gz' % kind)
    images_path = os.path.join(path, '%s-images-idx3-ubyte.gz' % kind)
    with gzip.open(labels_path, 'rb') as lbpath:
        labels = np.frombuffer(lbpath.read(), dtype=np.uint8, offset=8)
    with gzip.open(images_path, 'rb') as imgpath:
        images = np.frombuffer(imgpath.read(), dtype=np.uint8, offset=16).reshape(len(labels), 784)
    return images, labels
X_train, y_train = load_fashion_mnist('data_fashion_mnist/')
X_test, y_test = load_fashion_mnist('data_fashion_mnist/', kind='t10k')
# lấy số hàng của tập X_traint va X_test
m_train = 50000
m_test  = 10000
m_validation = 10000
### validation set
# Tạo list gồm 10000 số 
mask = list(range(m_train, m_train + m_validation)) 
# Tập con X_val gồm 10000 hình từ X_train
X_val = X_train[mask] 
# Lấy 10000 nhãn từ tập nhãn y_train
y_val = y_train[mask] 
### training set
# Tạo list gồm 50000 số từ 0 đến 49999
mask = list(range(m_train)) 
# Tạo lại tập X_train gồm 50000 hình 
X_train = X_train[mask] 
# Tạo lại tập nhãn y_train
y_train = y_train[mask] 
# Reshape data to rows
X_train = X_train.reshape(m_train, -1)
X_val   = X_val.reshape(m_validation, -1)
X_test  = X_test.reshape(m_test, -1)
print("X_train shape: ", X_train.shape)
print("y_train shape: ", y_train.shape)
print("X_val shape: ", X_val.shape)
print("y_val shape: ", y_val.shape)
print("X_test shape: ", X_test.shape)
print("y_test shape: ", y_test.shape)
```

- Đầu tiên ta load dữ liệu lên
- Lấy 10000 mẫu nhiên từ tập train để validate
- Lấy tập train từ 0->49999
- Đưa dữ liệu train, test, validate về dạng vector

- Lấy 1 vài data đẻ kiểm tra độ chính xác
``` python=
from PIL import Image
indices = list(np.random.randint(50000,size=5))
for i in range(5):
    im = Image.fromarray(X_train[indices[i]].reshape(28,28))
    im.save("data_fashion_mnist/image_" + str(i) +".png")
```
- Kết quả thu được
![](https://i.imgur.com/sK5y0B3.png)

### 3. Dữ liệu dạng rời rạc
```python=
import numpy as np        
import os                 
from random import shuffle 
from tqdm import tqdm    
from PIL import Image
TRAIN_DIR = 'dogs-vs-cats/train'
TEST_DIR  = 'dogs-vs-cats/test'
IMG_SIZE  = 50
def label_img(img):
    word_label = img.split('.')[0]
    if word_label == 'cat': 
        return 0
    elif word_label == 'dog': 
        return 1
    
def create_train_data():
    X_list = []
    y_list = []
    for img in tqdm(os.listdir(TRAIN_DIR)):
        label = label_img(img)
        path = os.path.join(TRAIN_DIR,img)
        
        img = Image.open(path)
        img = img.resize((IMG_SIZE,IMG_SIZE), Image.ANTIALIAS)
        img = np.asarray(img)
        
        X_list.append(img)
        y_list.append(label)
        
       
    X = np.array(X_list)
    y = np.array(y_list)
    
    np.save('dogs-vs-cats/X.npy', X)
    np.save('dogs-vs-cats/y.npy', y)
    
    return X, y
X,y = create_train_data()
print(X.shape)
print(y.shape)
```

- Các bước thực hiện như sau:
    - Đưa các LABEL về dang số để dễ phân loại
    - Thực hiện tạo data (data and label) để train
    - 