## 功能描述
GET Object 接口请求可以在 COS 的存储桶中将一个对象下载至本地。该操作需要请求者对存储桶有读取权限。 

## 请求

语法示例：
```
GET /<ObjectName> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.ccbcos.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (详细参见 [请求签名](https://github.com/ccbcloud/cos-api/blob/master/请求签名.md) 章节)

### 请求行
```
GET /<ObjectName> HTTP/1.1
```
该 API 接口接受 GET 请求。
#### 请求参数<style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>
包含所有请求参数的请求行示例：
```
GET /<ObjectName>?response-content-type=ContentType&response-content-language=ContentLanguage&response-expires=ContentExpires&response-cache-control=CacheControl&response-content-disposition=ContentDisposition&response-content-encoding=ContentEncoding HTTP/1.1
```
具体内容如下：

| 参数名称                         | 描述                               | 类型     | 必选   |
| :--------------------------- | :------------------------------- | :----- | :--- |
| response-content-type        | 设置响应头部中的 Content-Type 参数。        | String | 否    |
| response-content-language    | 设置响应头部中的 Content-Language 参数。    | String | 否    |
| response-expires             | 设置响应头部中的 Content-Expires 参数。     | String | 否    |
| response-cache-control       | 设置响应头部中的 Cache-Control 参数。       | String | 否    |
| response-content-disposition | 设置响应头部中的 Content-Disposition 参数。 | String | 否    |
| response-content-encoding    | 设置响应头部中的 Content-Encoding 参数。    | String | 否    |


**说明**

如果使用这些参数，那么请求必须要携带签名的，可以使用Authorization头部，也可以在URL参数中携带。匿名请求不允许携带这些参数 

### 请求头

#### 公共头部
该请求操作的实现使用公共请求头,了解公共请求头详细请参见 [公共请求头部](https://github.com/ccbcloud/cos-api/blob/master/公共请求头部.md) 章节。

#### 非公共头部
该请求操作推荐使用如下推荐请求头：

| 名称                  | 描述                                       | 类型     | 必选   |
| :------------------ | :--------------------------------------- | :----- | :--- |
| Range               | RFC 2616 中定义的指定文件下载范围，以字节（bytes）为单位      | String | 否    |
| If-Unmodified-Since | 如果文件修改时间早于或等于指定时间，才返回文件内容。否则返回 412 (precondition failed) | String | 否    |
| If-Modified-Since   | 当 Object 在指定时间后被修改，则返回对应 Object meta 信息，否则返回 304 | String | 否    |
| If-Match            | 当 ETag 与指定的内容一致，才返回文件。否则返回 412 (precondition failed) | String | 否    |
| If-None-Match       | 当 ETag 与指定的内容不一致，才返回文件。否则返回 304 (not modified) | String | 否    |

### 请求体
该请求的请求体为空。

## 响应

### 响应头
#### 公共响应头 
该响应使用公共响应头,了解公共响应头详细请参见 [公共响应头部](https://github.com/ccbcloud/cos-api/blob/master/公共响应头部.md) 章节。
#### 特有响应头
该请求操作的响应头具体数据为：

| 参数名称                | 描述                                       | 类型     |
| :------------------ | :--------------------------------------- | :----- |
| x-cos-meta- *       | 用户自定义的元数据                                | String |
| x-cos-object-type   | 用来表示 object 是否可以被追加上传，枚举值：normal 或者 appendable | String |

### 响应体

该响应体返回 Object 的文件内容。

## 实际案例

### 请求1
```
GET /123 HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.wh.ccbcos.com
Date: Wed, 28 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484212200;32557108200&q-key-time=1484212200;32557108200&q-header-list=host&q-url-param-list=&q-signature=11522aa3346819b7e5e841507d5b7f156f34e639
```


### 响应
```
HTTP/1.1 200 OK
Date: Wed, 28 Oct 2014 22:32:00 GMT
Content-Type: application/octet-stream
Content-Length: 16087
Connection: keep-alive
Accept-Ranges: bytes
Content-Disposition: attachment; filename="filename.jpg"
Content-Range: bytes 0-16086/16087
ETag: "9a4802d5c99dafe1c04da0a8e7e166bf"
Last-Modified: Wed, 28 Oct 2014 20:30:00 GMT
x-cos-object-type: normal
x-cos-request-id: NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ==

[Object]
```

### 请求2 携带response-xxx参数
```
GET /123?response-content-type=application%2fxml HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.wh.ccbcos.com
Date: Wed, 28 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484212200;32557108200&q-key-time=1484212200;32557108200&q-header-list=host&q-url-param-list=&q-signature=11522aa3346819b7e5e841507d5b7f156f34e639
```


### 响应
```
HTTP/1.1 200 OK
Date: Wed, 28 Oct 2014 22:32:00 GMT
Content-Type: application/xml
Content-Length: 16087
Connection: keep-alive
Accept-Ranges: bytes
Content-Disposition: attachment; filename="filename.jpg"
Content-Range: bytes 0-16086/16087
ETag: "9a4802d5c99dafe1c04da0a8e7e166bf"
Last-Modified: Wed, 28 Oct 2014 20:30:00 GMT
x-cos-object-type: normal
x-cos-request-id: NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ==

[Object]
```
