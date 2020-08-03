## 解析Http message 內容
### 狀況:flask 無法解析multipart/form-data，於是message body混雜boundary和影像raw data
### 使用requests_toolbelt套件

```python
  from requests_toolbelt.multipart import decoder
  content_type = request.content_type #取出content type
  message_body = request.data
  result = decoder.MultipartDecoder(message_body, content_type)
  raw_bmp = result.parts[0].content
```

## requests_toolbelt用於發送request
### multipart/form-data Encoder
### The main attraction is a streaming multipart form-data object, MultipartEncoder. Its API looks like this:
```python
from requests_toolbelt import MultipartEncoder
import requests

m = MultipartEncoder(
    fields={'field0': 'value', 'field1': 'value',
            'field2': ('filename', open('file.py', 'rb'), 'text/plain')}
    )

r = requests.post('http://httpbin.org/post', data=m,
                  headers={'Content-Type': m.content_type})
```
### Assuming `m` is one of the above檢查發送的訊息
```python
m.to_string()  # Always returns unicode
```
### post 圖片並接收
```python
    def post(self,args):
        import io
        from PIL import Image
        source_file = args.pop('source_file')
        image = source_file.read()
        image = Image.open(io.BytesIO(image))
        image.save('test.jpg')
        print(source_file.read())
        return "OK"
```
