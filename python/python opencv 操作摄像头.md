## python opencv 操作摄像头

**1.实验环境**

>1.win10
>
>2.python3.8
>
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

![image](https://user-images.githubusercontent.com/48900845/112761669-db797e80-902e-11eb-81e4-9545c2243094.png)


>作者info
>
>作者：DebugWuhen
>
>原创公众号：『DebugWuhen』，新号，专注于记录有趣的编程技术和有益的程序人生，期待你的关注。
>
>转载说明：务必注明来源（注明：来源于公众号：DebugWuhen， 作者：DebugWuhen）
>
>![image](https://user-images.githubusercontent.com/48900845/112752163-3b0e6480-9004-11eb-899d-66ddef749c2b.png)
