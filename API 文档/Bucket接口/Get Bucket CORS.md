## 功能描述
Get Bucket CORS 接口实现 Bucket 持有者在 Bucket 上进行跨域资源共享的信息配置。（CORS 是一个 W3C 标准，全称是"跨域资源共享"（Cross-origin resource sharing））。默认情况下，Bucket 的持有者直接有权限使用该 API 接口，Bucket 持有者也可以将权限授予其他用户。

## 请求

语法示例：
```
GET /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.ccbcos.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (详细参见 [请求签名](https://github.com/ccbcloud/cos-api/blob/master/请求签名.md) 章节)

### 请求行
~~~
GET /?cors HTTP/1.1
~~~
该 API 接口接受 GET 请求。

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
该响应体返回为 **application/xml** 数据，包含完整节点数据的内容展示如下：
```
<CORSConfiguration>
  <CORSRule>
    <ID></ID>
    <AllowedOrigin></AllowedOrigin>
    <AllowedMethod></AllowedMethod>
    <AllowedHeader></AllowedHeader>
    <MaxAgeSeconds></MaxAgeSeconds>
    <ExposeHeader></ExposeHeader>
  </CORSRule>
  <CORSRule>
    ...
  </CORSRule>
  ...
</CORSConfiguration>
```
具体的数据内容如下：<style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

|节点名称（关键字）|父节点|描述|类型|
|:---|:-- |:--|:--|
| CORSConfiguration |无| 说明跨域资源共享配置的所有信息，最多可以包含100条 CORSRule | Container |

Container 节点 CORSConfiguration 的内容：

|节点名称（关键字）|父节点|描述|类型|
|:---|:-- |:--|:--|
| CORSRule | CORSConfiguration | 说明单条配置的信息 |  Container |

Container 节点 CORSRule 的内容：

|节点名称（关键字）|父节点|描述|类型|
|:---|:-- |:--|:--|
| ID | CORSConfiguration.CORSRule | 配置规则的 ID，可选填|  String |
| AllowedOrigin | CORSConfiguration.CORSRule | 允许的访问来源，支持通配符 * </br>格式为：协议://域名[:端口]如：`http://www.ccb.com` |String |
| AllowedMethod | CORSConfiguration.CORSRule | 允许的 HTTP 操作，枚举值：GET，PUT，HEAD，POST，DELETE | Enum |
| AllowedHeader | CORSConfiguration.CORSRule | 在发送 OPTIONS 请求时告知服务端，接下来的请求可以使用哪些自定义的 HTTP 请求头部，支持通配符 * |  String |
| MaxAgeSeconds | CORSConfiguration.CORSRule | 设置 OPTIONS 请求得到结果的有效期 | Integer |
| ExposeHeader | CORSConfiguration.CORSRule | 设置浏览器可以接收到的来自服务器端的自定义头部信息 | String |

## 实际案例

### 请求
```
GET /?cors HTTP/1.1
Host: arlenhuangtestsgnoversion-1251668577.cos.wh.ccbcos.com
Date: Wed, 28 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484815944;32557711944&q-key-time=1484815944;32557711944&q-header-list=host&q-url-param-list=cors&q-signature=a2d28e1b9023d09f9277982775a4b3b705d0e23e
```

### 响应
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 345
Connection: keep-alive
Date: Wed, 28 Oct 2016 21:32:00 GMT
Server: ccb-cos
x-cos-request-id: NTg4MDdlNGZfNDYyMDRlXzM0YWFfZTBh

<CORSConfiguration> 
  <CORSRule> 
    <ID>1234</ID>  
    <AllowedOrigin>http://www.ccb.com</AllowedOrigin>  
    <AllowedMethod>PUT</AllowedMethod>  
    <AllowedHeader>x-cos-meta-test</AllowedHeader>  
    <ExposeHeader>x-cos-meta-test1</ExposeHeader>  
    <MaxAgeSeconds>500</MaxAgeSeconds> 
  </CORSRule> 
</CORSConfiguration>
```

