## python 初试opencv
**1.实验环境**
>1.win10
>2.python3.8
>3.opencv-4.4.0.46
>4.matplotlib-3.3.2

**2.源码**

main.py

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
import cv2
from pylab import *

# 载入图像
im = cv2.imread('1.jpg')

# 颜色空间转换
gray = cv2.cvtColor(im, cv2.COLOR_BGR2GRAY)

# 显示原始图像
fig = plt.figure()
subplot(121)
plt.gray()
imshow(im)
title(u'彩色图')
axis('off')
# 显示灰度化图像
plt.subplot(122)
plt.gray()
imshow(gray)
title(u'灰度图')
axis('off')

show()
```

**效果图**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201104143655820.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
