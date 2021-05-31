# HÀM SIGMOID
## 1. Cách dùng
- Được dùng để phân loại binary
    - >T (thường là 0.5) thì là loại 0
    - <T thì là loại 1
![](https://i.imgur.com/hGLFAtk.png)

- CÁCH DÙNG: output của **linear regression** được đưa vào làm input của hàm **SIG MOID** để phân loại cho giá trị khoảng [0,1]
![](https://i.imgur.com/kopc0jo.png)

## 2. Tính Loss dùng binary cross entropy
- Biến đổi hàm LOSS thành dạng vector J:
![](https://i.imgur.com/mSoj1MD.png)

- Đạo hàm hàm J ta được: (h-y)x
![](https://i.imgur.com/KnNldWV.png)

- Đạo hàm cho từng tham số và cập nhật:
![](https://i.imgur.com/kmSdFNY.png)
