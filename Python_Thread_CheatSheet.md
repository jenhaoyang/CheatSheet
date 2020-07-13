# 開Thread
```python
class OpenBrowser(Thread):

    def __init__(self):
        super(OpenBrowser, self).__init__()

    def notResponding(self):
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        return sock.connect_ex(('127.0.0.1', 5000))

    def run(self):
        while self.notResponding():
            print('Did not respond')
        print('Responded')
        webbrowser.open_new('http://127.0.0.1:5000/')
        
if __name__ == '__main__':
    th = OpenBrowser()
    th.start()
```
