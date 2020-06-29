pipenv

venv

pew

virtualenv



### pip反安裝所有套件
pip freeze > requirement.txt
pip uninstall -r requirement.txt -y



### OpenCV和PIL互轉
OpenCV转换成PIL.Image格式：
```python
import cv2  
from PIL import Image  
import numpy  
  
img = cv2.imread("plane.jpg")  
cv2.imshow("OpenCV",img)  
image = Image.fromarray(cv2.cvtColor(img,cv2.COLOR_BGR2RGB))  
image.show()  
cv2.waitKey()  
``` 

PIL.Image转换成OpenCV格式：
```python
import cv2  
from PIL import Image  
import numpy  
  
image = Image.open("plane.jpg")  
image.show()  
img = cv2.cvtColor(numpy.asarray(image),cv2.COLOR_RGB2BGR)  
cv2.imshow("OpenCV",img)  
cv2.waitKey()
```
————————————————
版权声明：本文为CSDN博主「_yuki_」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_19707521/java/article/details/78367617
