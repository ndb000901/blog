## python opencv 操作摄像头
**1.实验环境**
>1.win10
>2.python3.8
>3.opencv-4.4.0.46

**2.源码**

main.py

```
import cv2
import numpy as np

cap = cv2.VideoCapture(0)
while 1:
    # get a frame
    ret, frame = cap.read()
    # show a frame
    cv2.imshow("capture", frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
cap.release()
cv2.destroyAllWindows()
```

**3.效果**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201104145044659.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzOTM4MDUy,size_16,color_FFFFFF,t_70#pic_center)
