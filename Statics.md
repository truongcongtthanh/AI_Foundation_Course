# Statistic
## 1. Mean (Trung bình)
![](https://i.imgur.com/qkvdGiB.png)
Application: Blur photo

![](https://i.imgur.com/KRYAgOI.png)
Mean is Correlation with Kernel w = 1/n

![](https://i.imgur.com/7RFBUsp.png)
new image is smaller the original image

![](https://i.imgur.com/gP2D3WG.png)
Application: blur image
use cv2.fillter2D(image, cv2.CV_8U, kernel) to calculate mean for each pixel

![](https://i.imgur.com/CyPVWVN.png)
Video have the blur face

```python=
import cv2
import numpy as np

# To capture video from webcam. 
cap = cv2.VideoCapture(0)

# select region
while True:
    # Read the frame and Convert to grayscale
    _, img = cap.read()
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    
    top_left = (200,300)
    bottom_right = (400,400)
    cv2.rectangle(img, top_left, bottom_right, (0, 255, 0), 2)

    
    # Display
    cv2.imshow('img', img)
    
    # Stop if escape key is pressed
    if cv2.waitKey(33) == ord('a'):  
        break

template = gray[300:400, 200:400]
w, h = template.shape[::-1]
cv2.imshow('template', template)
cv2.waitKey(0)

while True:
    # Read the frame and Convert to grayscale
    _, img = cap.read()
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
        
    corr_map = cv2.matchTemplate(gray, template, cv2.TM_CCOEFF_NORMED)
    min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(corr_map) 

    # take minimum
    top_left = max_loc
    bottom_right = (top_left[0] + w, top_left[1] + h)

    # draw 
    cv2.rectangle(img, top_left, bottom_right, (0, 255, 0), 2)

    
    # Display
    cv2.imshow('img', img)
    
    # Stop if escape key is pressed
    if cv2.waitKey(33) == ord('a'):  
        break

# Release the VideoCapture object
cap.release()
cv2.destroyAllWindows()
```
![](https://i.imgur.com/Yzcc7oC.png)

## 2. Median (Trung vị - lấy giá trị số ở trường hoặc trung bình 2 số ở giữa nếu số phần tử chẳn)

![](https://i.imgur.com/t8oQiBy.png)
Apply for Image Denoising (Khử nhiễu) problem

```python=
import numpy as np
import cv2

img1 = cv2.imread('mrbean_noise.jpg')
img2 = cv2.medianBlur(img1, 3)

# show images
cv2.imshow('img1', img1)
cv2.imshow('img2', img2)

# waiting for any keys pressed and close windows
cv2.waitKey(0)
cv2.destroyAllWindows()
```
## 3. Range
![](https://i.imgur.com/oZKXglO.png)

### Histogram
![](https://i.imgur.com/qo3pl5J.png)
![](https://i.imgur.com/BPYZsjy.png)
![](https://i.imgur.com/zznRlua.png)
![](https://i.imgur.com/VRi4U8e.png)
### b(new) =  [255*H[b] + 0.5]

![](https://i.imgur.com/oLvFL00.png)
![](https://i.imgur.com/f3XNL42.png)
Result

## 4. Variance (phương sai)
![](https://i.imgur.com/dMfRUug.png)
![](https://i.imgur.com/T6urhxp.png)
Apply for finding information image (texture)

![](https://i.imgur.com/C46tU62.png)
are with many fluctuations will have standard deviation value is big

![](https://i.imgur.com/BZxZ9RA.png)
```python=
import numpy as np
import cv2
import math
from scipy.ndimage.filters import generic_filter

img  = cv2.imread('img.jpg',1)
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
cv2.imwrite('edge_s1.jpg', gray)

x = gray.astype('float')
x_filt = generic_filter(x, np.std, size=7)
cv2.imwrite('edge_s2.jpg', x_filt)

x_filt[x_filt < 20] = 0
cv2.imwrite('edge_s3.jpg', x_filt)

maxv = np.max(x_filt)
print(maxv)

x_filt = x_filt*2.5
cv2.imwrite('edge_s4.jpg', x_filt)
```

![](https://i.imgur.com/9lBjxcD.png)

## 5. Correlation Coefficient
![](https://i.imgur.com/VWhyx6r.png)

![](https://i.imgur.com/RzKy6I0.png)
compare the similarity between 2 image

#**Template matching**  
use to detect template in image  
![](https://i.imgur.com/9nOChBq.png)  
How to make it:  
1. Convert color image to gay image   
=> Reduce light noise  
![](https://i.imgur.com/daOqZg1.png)  
2. Use function to solve template matching  
```python=
corr_map = cv2.matchTemplate(gray, template, cv2.TM_CCOEFF_NORMED)
```
![](https://i.imgur.com/xZAYeDI.png)  
This is result after use function (white point)  

you can color the image for easy viewing by  
```python=
corr_map = cv2.applyColorMap(corr_map, cv2.COLORMAP_JET)
```
![](https://i.imgur.com/ZGfL4jE.png)  
<p align="center">(Red point)<p align="center">  

```python=
cv2.rectangle(image, top_left, bottom_right, (0, 255, 0), 2)
```  
![](https://i.imgur.com/ZRuuAWI.png)  
```python=
# template matching
import cv2
import numpy as np
from matplotlib import pyplot as plt

# Load image and convert to grayscale
image = cv2.imread('image.png',1)
gray  = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

template = cv2.imread('template.png',0)
w, h = template.shape[::-1]

# Apply template Matching
corr_map = cv2.matchTemplate(gray, template, cv2.TM_CCOEFF_NORMED)
min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(corr_map) 

# take minimum
top_left = max_loc
bottom_right = (top_left[0] + w, top_left[1] + h)

# draw 
cv2.rectangle(image, top_left, bottom_right, (0, 255, 0), 2)

# save corr map in grayscale
corr_map = (corr_map+1.0)*127.5
corr_map = corr_map.astype('uint8') 
cv2.imwrite('corr_map_grayscale.png', corr_map)

# applyColorMap
corr_map = cv2.applyColorMap(corr_map, cv2.COLORMAP_JET)

# save results
cv2.imwrite('corr_map_color.png', corr_map)
cv2.imwrite('result.png', image)
```
<p align="center">Source code<p align="center">

<p align="right">Slide and source code from Dinh Quang Vinh teacher<p align="right">

