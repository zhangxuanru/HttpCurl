# HttpCurl.class.php
Curl模拟Http工具类

可实现模拟GET、POST请求, 支持上传文件/自定义header头

## How To Use.

使用composer
```bash
composer require gaoming13/http-curl
```

```php
use Gaoming13\HttpCurl\HttpCurl;
```

### v2.2

```php
HttpCurl::request('http://example.com/', 'get');

HttpCurl::request('http://example.com/?a=123', 'get', array(
	'b' => 456
));

HttpCurl::request('http://example.com/', 'post', array(
    'user_uid' => 'root',
    'user_pwd' => '123456'
));

HttpCurl::request('http://example.com/', 'post', array(
	'file1' => '@/data/sky.jpg',
	'file2' => '@/data/bird.jpg'
));

HttpCurl::request('http://example.com/', 'post', array(
	'file1' => '@G:\wamp\www\data\sky.jpg',
	'file2' => '@G:\wamp\www\data\bird.jpg'
));

HttpCurl::request('http://example.com/', 'post', array(
    'user_uid' => 'root',
    'user_pwd' => '123456'
), array('Content-Type:application/json'));
```

```
list($body, $header, $status, $errno, $error) = \Gaoming13\HttpCurl\HttpCurl::request('http://www.example.com/', 'get');
```

$body 响应正文

```
<!doctype html>
<html>
<head>
    <title>Example Domain</title>
	...	
```

$header 响应头

```
HTTP/1.1 200 OK
Accept-Ranges: bytes
Cache-Control: max-age=604800
Content-Type: text/html
Date: Thu, 14 Apr 2016 08:42:35 GMT
Etag: "359670651+gzip"
Expires: Thu, 21 Apr 2016 08:42:35 GMT
Last-Modified: Fri, 09 Aug 2013 23:54:35 GMT
Server: ECS (rhv/818F)
Vary: Accept-Encoding
X-Cache: HIT
x-ec-custom-error: 1
Content-Length: 1270
```

$status 该次请求的状态

```
'url' => string 'http://www.example.com/' (length=23)
'content_type' => string 'text/html' (length=9)
'http_code' => int 200
'header_size' => int 349
'request_size' => int 54
'filetime' => int -1
'ssl_verify_result' => int 0
'redirect_count' => int 0
'total_time' => float 0.512924
'namelookup_time' => float 0.064248
'connect_time' => float 0.270048
'pretransfer_time' => float 0.270202
'size_upload' => float 0
'size_download' => float 1270
'speed_download' => float 2476
'speed_upload' => float 0
'download_content_length' => float 1270
'upload_content_length' => float 0
'starttransfer_time' => float 0.510861
'redirect_time' => float 0
'redirect_url' => string '' (length=0)
'primary_ip' => string '93.184.216.34' (length=13)
'certinfo' => 
array (size=0)
  empty
'primary_port' => int 80
'local_ip' => string '192.168.248.129' (length=15)
'local_port' => int 54402
```

$errno 错误码

```
0
```

$error 错误信息

```
```

### v1

```php
require 'v1/HttpCurl.class.php';

// GET请求
HttpCurl::get('http://api.example.com/');

// GET请求, 并json_decode返回的数组
HttpCurl::get('http://api.example.com/?a=123&b=456', 'json');

// POST请求
HttpCurl::post('http://api.example.com/?a=123', array(
	'abc'=>'123', 
	'efg'=>'567'
));
HttpCurl::post('http://api.example.com/', '这是post原始内容', 'json');

// POST请求, 文件上传
HttpCurl::post('http://api.example.com/', array(
	'file1'=>'@/data/sky.jpg',
	'file2'=>'@/data/bird.jpg',
));
```

## License

MIT
