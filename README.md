#浏览器缓存机制有以下两种：

一. 非Http协议定义的缓存机制

如 META HTTP-EQUIV="Pragma" CONTENT="no-cache" 告诉浏览器不要缓存，每次请求都去服务器拉取;

二. Http协议定义的缓存机制

respond响应头信息中的Expired/Cache-Control如果没过期，直接读取缓存文件，如果过期，就会从响应头信息中查找是否有Etag值，

如果有Etag值，就会向服务器端发送带有If-None-Math(Etag值)的请求，如果与服务器端的Etag相等，就会返回304，然后读取缓存文件，如果不相等，就去服务器拉取，返回200。


如果没有Etag值，就会去响应头信息中找到Last-Modifed,然后向服务器端发送带有If-Modifed-Since(Last-Modifed值)的请求,如果与服器端的Last-Modifed相等，就会返回304，然后读取缓存文件，如果不相等，就去服务器拉取，返回200。


#无法被浏览器缓存的请求:

1.HTTP信息头中包含Cache-Control:no-cache，pragma:no-cache（HTTP1.0），或Cache-Control:max-age=0等告诉浏览器不用缓存的请求

2.POST请求无法被缓存

