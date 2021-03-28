## python 初试opencv

**1.实验环境**

>1.win10
>
>2.python3.8
>
>3.opencv-4.4.0.46
>
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

![image](https://user-images.githubusercontent.com/48900845/112761716-2dba9f80-902f-11eb-925c-aec4491487ee.png)


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
