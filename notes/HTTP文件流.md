# HTTP文件流

* http请求头中的content-length 和 Transfer-Encoding:chunked
    
    通常来说，http协议中使用Content-Length这个头来告知我们数据的长度，然后，在数据吓醒的过程中，Content-Length的方式要预先在服务器中缓存所有数据，然后所有数据再一股脑的发给客户端，如果要一边产生数据，一边发给客户端，web服务器就需要使用Transfer-Encoding: chunked 这样的方式要代替Content-Length （Node最大的头大小是80KB）
    
* http前后端交互类型采用Content-Type:application/octet-stream的作用

    二进制文件
    
* application/x-www-form-urlencoded

    最常见的POST提交数据的方式，浏览器的原生form表单，如果不设置enctype属性，那么最终会以application/x-www-form-urlencoded方式提交数据，
    
    ```
    POST http://www.example.com HTTP/1.1
    Content-Type: application/x-www-form-urlencoded;charset=utf-8
    
    title=test&sub%5B%5D=1&sub%5B%5D=2&sub%5B%5D=3
    ```
    
* application/multipart/form-data

    我们使用表单上传文件时，必须让 <form> 表单的 enctype 等于 multipart/form-data
    
    ```
    POST http://www.example.com HTTP/1.1
    Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryrGKCBY7qhFd3TrwA
    
    ------WebKitFormBoundaryrGKCBY7qhFd3TrwA
    Content-Disposition: form-data; name="text"
    
    title
    ------WebKitFormBoundaryrGKCBY7qhFd3TrwA
    Content-Disposition: form-data; name="file"; filename="chrome.png"
    Content-Type: image/png
    
    PNG ... content of chrome.png ...
    ------WebKitFormBoundaryrGKCBY7qhFd3TrwA--

    ```

