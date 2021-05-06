## opencv处理图片

**1.实验环境**

>1.manjaro21-gnome
>
>2.python3.9
>
>3.opencv-python-4.5.1.48
>
>4.numpy-1.20.2
>

**2.加载、显示、保存图片**

```
# 加载、显示、保存图片
import cv2
img = cv2.imread("1.jpeg")
cv2.imwrite("save.png", img)
cv2.imshow("img", img)
cv2.waitKey()
```

**2.获取图片宽、高、通道数**

```
# 获取图片宽、高、通道数
import cv2

img = cv2.imread("1.jpeg")
print(img.shape)
```

**输出结果**

返回图片的高、宽、通道，若图像为非彩色图，则不返回通道值。

```
(750, 500, 3)
```

**3.图像缩放**

图像缩放使用cv2.resize()函数，第三个参数定义了缩放插值的方法。

|参数|说明|
|----|----|
|INTER_NEAREST|最近邻插值法|
|INTER_LINEAR|双线性插值法（默认）|
|INTER_AREA|基于局部像素的重采样|
|INTER_CUBIC|基于4x4像素邻域的3次插值法|
|INTER_LANCZOS4|基于8x8像素邻域的Lanczos插值|

```
# 图像缩放

import cv2

img = cv2.imread("1.jpeg")
cv2.imshow("img", img)
img1 = cv2.resize(img, (100, 600), cv2.INTER_AREA)
hight, width = img.shape[0:2]
img2 = cv2.resize(img, (width, hight))
cv2.imshow("img1", img1)
cv2.imshow('img2', img2)
cv2.waitKey()
```

**4.图片旋转**

**main.py**

```
import numpy as np
import argparse
import imutils
import cv2

ap = argparse.ArgumentParser()
ap.add_argument("-i", "--image", required=True,
                help="Path to the image")
args = vars(ap.parse_args())

image = cv2.imread(args["image"])
cv2.imshow("Original", image)

(h, w) = image.shape[:2]
center = (w // 2, h // 2)

M = cv2.getRotationMatrix2D(center, 45, 1.0)
rotated = cv2.warpAffine(image, M, (w, h))
cv2.imshow("Rotated by 45 Degrees", rotated)

M = cv2.getRotationMatrix2D(center, -90, 1.0)
rotated = cv2.warpAffine(image, M, (w, h))
cv2.imshow("Rotated by -90 Degrees", rotated)

rotated = imutils.rotate(image, 180)
cv2.imshow("Rotated by 180 Degrees", rotated)
cv2.waitKey(0)
```

**imutils.py**

rotate()第一个参数为需要处理的图片,第二个为角度，第三个为旋转中心，默认为图片中心，第四个为规模，默认1.0。

```
import cv2
def rotate(image, angle, center=None, scale=1.0):
    (h, w) = image.shape[:2]
    if center is None: 
        center = (w // 2, h // 2)

    M = cv2.getRotationMatrix2D(center, angle, scale)

    rotated = cv2.warpAffine(image, M, (w, h))
    return rotated
```

**5.图像轮廓检测**

```
# 图片轮廓检测
import cv2
import numpy as np

img = cv2.imread('1.jpeg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)                        #转换为灰度图像
ret, binary = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)        #转换为二值图像
contours, hierarchy = cv2.findContours(binary, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)#提取轮廓
cv2.drawContours(img, contours, -1, (0, 0, 255), 2)
cv2.imshow("img", img)
cv2.waitKey()
```
