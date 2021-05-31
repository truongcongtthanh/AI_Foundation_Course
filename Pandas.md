# Pandas 
## 1. Cơ bản
### 1.1 Khởi tạo
``` python=
# import pandas
import pandas as pd
#tạo pd series
fruits = pd.Series(data = [30, 6, 'Yes', 'No'], 
                   index = ['mango', 'apple', 'pineaple', 'orange'])
print(fruits)
```
![](https://i.imgur.com/U3PWdib.png)

:arrow_right: Về cơ bản thì **PANDAS SERIES** như **DICTIONARY** 

### 1.2 Một số thuộc tính cơ bản:
``` python=
import pandas as pd
#tạo pd series
fruits = pd.Series(data = [30, 6, 'Yes', 'No'], 
                   index = ['mango', 'apple', 'pineaple', 'orange'])
#show độ dài, ở đây chỉ có 1 chiều nên kết quả trả về (4,)
print('\n Series has shape:', fruits.shape)
#ndim để xác định nó là pandas Series(1) hay DataFranme(2)
print('\n Series has dimension:', fruits.ndim)
# trả về size của Series
print('\n Series has a total of', fruits.size, 'elements')
#check xem có mango không
x = 'mango' in fruits
print('\n Is mango available?: ', x)
```
![](https://i.imgur.com/9N0qoSd.png)

- .ndim: trả về
    - 1: là series
    - 2: là dataframe
- Biến **x** cho phép ta tìm trong index

## 2. Cách truy cập và thao tác với Pandas Series
### 1. Truy cập index label (dùng .loc)
``` python=
# import pandas
import pandas as pd
#tạo pd series
fruits = pd.Series(data = [30, 6, 'Yes', 'No'], 
                   index = ['mango', 'apple', 'pineaple', 'orange'])
# sử dụng một nhãn chỉ mục duy nhất
print('\n How many apples do we need to buy:', fruits['apple'])
# chúng ta có thể truy cập nhiều nhãn chỉ mục
print('\n Do we need orange and apples:\n', fruits[['orange', 'apple']])
# chúng tôi sử dụng loc để truy cập nhiều nhãn chỉ mục
print('\n How many mango and apples do we need to buy:\n', fruits.loc[['mango', 'apple']])
# Chúng ta truy cập các phần tử trong fruits bằng các chỉ số bằng số:
print('\n How many eggs and apples do we need to buy:\n',  fruits[[0, 1]]) 
# Chúng ta sử dụng một chỉ số số âm
print('\n Do we need orange:\n', fruits[[-1]])
# Chúng tôi sử dụng một chỉ số số duy nhất
print('\n How many mangos do we need to buy:', fruits[0])
# chúng tôi sử dụng iloc để truy cập nhiều chỉ số
print('\n Do we need mangos and apples:\n', fruits.iloc[[1, 2]])
```
![](https://i.imgur.com/9GA6Qbb.png)

- Dùng fruits[['orange','apple']] cho kết quả tương tự khi dùng fruits.loc[['orange','apple']]
- Tương tự ta có thể dùng fruits[[0,1]] = fruits.iloc[[0,1]]
- Hoặc là fruits[-1] để lấy giá trị cuối cùng..

### 2. Xoá item bằng cách dùng drop - fruits.drop('apple', inplace = True)
![](https://i.imgur.com/7McWX7x.png)

### 3. Phép toán số học trên Pandas Series
- Như khi làm toán với **NUMPY**
![](https://i.imgur.com/iRFMpP0.png)
- Kể cả các phép **Luỹ Thừa**, **Lấy căn**..
![](https://i.imgur.com/nTDfjMu.png)

- Thay đổi trong từng phần tử
![](https://i.imgur.com/1wALBXt.png)

## 3. PANDAS Dataframe
- Cấu trúc dữ liệu 2 chiều, tương tự như excel với hàng và cột được gán nhãn (Là 1 bảng lưu trữ dữ liệu)

- Cách chuyển Dataframe
``` python=
# import pandas
import pandas as pd
# We create a dictionary of Pandas Series 
items = {'Bob' : pd.Series(data = [245, 25, 55], 
                           index = ['bike', 'pants', 'watch']),
         'Alice' : pd.Series(data = [40, 110, 500, 45], 
                             index = ['book', 'glasses', 'bike', 'pants'])}
# We create a Pandas DataFrame by passing it a dictionary of Pandas Series
shopping_carts = pd.DataFrame(items)
# We display the DataFrame
shopping_carts
```
- Kết quả: Ghép tương ứng theo label
![](https://i.imgur.com/Ugr18JW.png)

- Nếu không tạo **INDEX cho pandas SERIES** thì kết quả sẽ là: ghép tương ứng theo chỉ mục
![](https://i.imgur.com/5KZjPRT.png)

- Một số thuộc tính:
    - .values: để xem data
    - .index: để xem các chỉ mục
    - .columns: Để xem các cột
![](https://i.imgur.com/TlJLIf3.png)

- Ngoài ra, còn có thể tạo Dataframe bằng **LIST** thay cho **pd Series**
![](https://i.imgur.com/5RrbRUR.png)

- Dùng **DICTIONARY** để tạo Dataframe với các rows mạc định là 0,1..
![](https://i.imgur.com/ZZPtC3i.png)

- Tự thiết đặt rows bằng cách:
![](https://i.imgur.com/8itXpsG.png)

- Truy xuất theo label để lấy **COLUMN** và .loc để lấy **ROWS**
![](https://i.imgur.com/PtXiBKR.png)

- Thêm một COLUMN
![](https://i.imgur.com/zc4zBx2.png)
![](https://i.imgur.com/jGU5sPp.png)

- Thêm một ROW: bằng cách tạo 1 row DF mới và add vào DF cũ
![](https://i.imgur.com/L2kfhkk.png)
![](https://i.imgur.com/tfcij4V.png)

### 3.2 Xoá trong DF
- .pop(): Dùng để xoá cột
- .drop(): Xoá cả cột và hàng bằng cách thay **axis**:
    - axis = 1 -> cột
    - axis = 0 -> hàng
![](https://i.imgur.com/3kxBwZk.png)
![](https://i.imgur.com/vXCnyof.png)

### 3.3 Xử lí NaN
- Bảng dữ liệu ta có
![](https://i.imgur.com/jCvUILT.png)

- In ra các COLUMN có giá trị NaN
![](https://i.imgur.com/TVL4d17.png)

- Tổng số NaN
![](https://i.imgur.com/RA4xVAD.png)

- Thay các giá trị NaN bằng các giá trị 0
![](https://i.imgur.com/weQtlyA.png)

## 3. Đọc file CSV (thường là excel)
- Dùng pd.read_csv('name_file')
![](https://i.imgur.com/rUy4d3T.png)

- Show 1 số đại diện dùng head(N=5), tail(N=5)
![](https://i.imgur.com/x7rnT0S.png)

