## 功能描述
Head Bucket 请求可以确认该 Bucket 是否存在，是否有权限访问。Head 的权限与 Read 一致。当该 Bucket 存在时，返回 HTTP 状态码 200；当该 Bucket 无访问权限时，返回 HTTP 状态码 403；当该 Bucket 不存在时，返回 HTTP 状态码 404。
>备注： 目前我们还没有公开获取 Bucket 属性的接口（即可以返回ACL等信息）。

## 请求

语法示例：
```
HEAD / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.ccbcos.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (详细参见 [请求签名](https://github.com/ccbcloud/cos-api/blob/master/请求签名.md) 章节)

### 请求行
```
HEAD / HTTP/1.1
```
该 API 接口接受 HEAD 请求。

### 请求头

#### 公共头部
该请求操作的实现使用公共请求头,了解公共请求头详细请参见 [公共请求头部](https://github.com/ccbcloud/cos-api/blob/master/公共请求头部.md) 章节。

#### 非公共头部
该请求操作无特殊的请求头部信息。

### 请求体
该请求的请求体为空。

## 响应

### 响应头
#### 公共响应头  
该响应使用公共响应头,了解公共响应头详细请参见 [公共响应头部](https://github.com/ccbcloud/cos-api/blob/master/公共响应头部.md) 章节。
#### 特有响应头 
该响应无特殊的响应头。

### 响应体
该响应体返回为空。

## 实际案例

### 请求
```
HEAD / HTTP/1.1
Host: zuhaotestsgnoversion-1251668577.cos.wh.ccbcos.com
Date: Thu, 27 Oct 2015 20:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484640517;32557536517&q-key-time=1484640517;32557536517&q-header-list=host&q-url-param-list=&q-signature=7bedc2f84a0a3d29df85fe727d0c1e388c410376
```

### 响应
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Thu, 27 Oct 2015 20:32:00 GMT
x-cos-request-id: NTg3ZGQxNDNfNDUyMDRlXzUyOWNfMjY5

```
