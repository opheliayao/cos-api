## ccbcloud cos api

对象存储的 XML API 是一种轻量级的，无连接状态的接口。您可以调用此套接口直接通过 http/https 发出请求和接受响应，从而实现与云平台对象存储（COS）后台进行交互操作。此套API的请求和响应内容都为XML格式。

在查阅其他的 API 文档之前，首先请详细阅读签名鉴权 。

## 基本信息

本部分介绍是为了您更有效的使用 COS ，而必须要了解的主要概念和术语。

| 名称          | 描述                                       |
| ----------- | ---------------------------------------- |
| AppID | 开发者访问 COS 服务时拥有的用户维度唯一资源标识，用以标示资源。       |
| SecretID    | SecretID 是开发者拥有的项目身份识别 ID，用以身份认证         |
| SecretKey   | SecretKey 是开发者拥有的项目身份密钥。                 |
| Bucket      | 存储桶是 COS 中用于存储数据的容器，是用户存储在 Appid 下的第一级目录，每个对象都存储在一个存储桶中。 |
| Object      | 对象是 COS 中存储的具体文件，是存储的基本实体。               |
| Region      | 域名中的地域信息，枚举值：wh（武汉） |

## 快速入门

要使用对象存储 API，需要先执行以下步骤：

1. 获取 Appid、SecretID、SecretKey 内容
2. 编写一个 签名鉴权 算法程序（或使用任何一种服务端 SDK）
3. 计算签名，调用 API 执行操作

## Header介绍
公共相应头部请参考 [公共响应头部](https://github.com/ccbcloud/cos-api/blob/master/%E5%85%AC%E5%85%B1%E5%93%8D%E5%BA%94%E5%A4%B4%E9%83%A8.md)。
公共请求头部请参考 [公共请求头部](https://github.com/ccbcloud/cos-api/blob/master/%E5%85%AC%E5%85%B1%E8%AF%B7%E6%B1%82%E5%A4%B4%E9%83%A8.md)。

## 请求签名
使用对象存储服务 COS 时，可通过 RESTful API 对 COS 发起 HTTP 匿名请求或 HTTP 签名请求，对于签名请求，COS 服务器端将会进行对请求发起者的身份验证。
请求签名请参考 [请求签名](https://github.com/ccbcloud/cos-api/blob/master/%E8%AF%B7%E6%B1%82%E7%AD%BE%E5%90%8D.md)。


## 错误码
请求出错时返回的错误码和对应错误信息请参考[错误码](https://github.com/ccbcloud/cos-api/blob/master/%E9%94%99%E8%AF%AF%E7%A0%81.md)
