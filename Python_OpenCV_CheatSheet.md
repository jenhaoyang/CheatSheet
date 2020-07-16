## 圖片載入np
```python
import PIL.Image
def load_image_file(file, mode='RGB'):
    """
    Loads an image file (.jpg, .png, etc) into a numpy array
    :param file: image file name or file object to load
    :param mode: format to convert the image to. Only 'RGB' (8-bit RGB, 3 channels) and 'L' (black and white) are supported.
    :return: image contents as numpy array
    """
    im = PIL.Image.open(file)
    if mode:
        im = im.convert(mode)
    return np.array(im)
```

## 從http message body 取得的八位元(hex)影像資料轉換成圖片
#### 使用Pillow 和 BytesIO
```python
    from PIL import Image
    from io import BytesIO
    import codecs

    gif_bytes_io = BytesIO()  # or io.BytesIO()

    # store the gif bytes to the IO and open as image
    gif_bytes_io.write(raw_bmp)
    image = Image.open(gif_bytes_io)
    image.show()
```

## OpenCV和PIL互轉

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


# resize
```python
#column = w    row = height
(row,column,channel)=cv2_img.shape
resize_ratio=413/column
resize_column = int(column*resize_ratio)
resize_row = int(resize_column*(row/column))
cv2_img = cv2.resize(cv2_img,(resize_column, resize_row),interpolation = cv2.INTER_AREA)
```
