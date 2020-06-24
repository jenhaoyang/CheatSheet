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
