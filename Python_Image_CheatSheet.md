## 從http message body 取得的八位元(hex)影像資料轉換成圖片
## 使用Pillow 和 BytesIO
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
