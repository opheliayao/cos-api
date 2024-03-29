## 功能描述
Abort Multipart Upload 用来实现舍弃一个分块上传并删除已上传的块。当您调用 Abort Multipart Upload 时，如果有正在使用这个 Upload Parts 上传块的请求，则 Upload Parts 会返回失败。当该 UploadId 不存在时，会返回 404 NoSuchUpload。

><font color="#0000cc">**注意：** </font>
>建议您及时完成分块上传或者舍弃分块上传，因为已上传但是未终止的块会占用存储空间进而产生存储费用。

## 请求

语法示例：
```
DELETE /ObjectName?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.ccbcos.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (详细参见 [请求签名](https://github.com/ccbcloud/cos-api/blob/master/请求签名.md) 章节)

### 请求行
```
DELETE /ObjectName?uploadId=UploadId HTTP/1.1
```
该 API 接口接受 DELETE 请求。
#### 请求参数
包含所有请求参数的请求行示例：
```
DELETE /ObjectName?uploadId=UploadId HTTP/1.1
```
具体内容如下：<style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

|参数名称|描述|类型|必选|
|---|---|---|---|
|uploadId|标识本次分块上传的 ID。<br>使用 Initiate Multipart Upload 接口初始化分片上传时会得到一个 uploadId，该 ID 不但唯一标识这一分块数据，也标识了这分块数据在整个文件内的相对位置 |String|是|

### 请求头

#### 公共头部
该请求操作的实现使用公共请求头,了解公共请求头详细请参见 [公共请求头部](https://github.com/ccbcloud/cos-api/blob/master/公共请求头部.md) 章节。

#### 非公共头部
该请求操作无特殊的请求头部信息。


### 请求体
该请求的请求体空。

## 响应

### 响应头
#### 公共响应头 
该响应使用公共响应头,了解公共响应头详细请参见 [公共响应头部](https://github.com/ccbcloud/cos-api/blob/master/公共响应头部.md) 章节。
#### 特有响应头
该请求操作无特殊的响应头。


### 响应体
该请求的响应体为空


## 实际案例

### 请求
```
DELETE /ObjectName?uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: arlenhuangtestsgnoversion-1251668577.cos.wh.ccbcos.com
Date: Tue, 26 Oct 2013 21:22:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484728626;32557624626&q-key-time=1484728626;32557624626&q-header-list=host&q-url-param-list=uploadId&q-signature=2d3036b57cade4a257b48a3a5dc922779a562b18

```

### 响应
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Tue, 26 Oct 2013 21:22:00 GMT
Server: ccb-cos
x-cos-request-id: NTg3ZjI5MzlfOTgxZjRlXzZhYjNfMjBh

```
