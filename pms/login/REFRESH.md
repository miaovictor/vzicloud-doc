# 刷新临时AccessKey

## 接口描述

刷新临时AccessKey，在当前AccessKey有效期的第1小时30分至2小时期间，通过调用此接口，可以获取一个新的2小时有效期的AccessKey；对于非临时AccessKey调用此接口会失败。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | GET | /v2/pms/users/refresh_accesskey

### URL参数

参数 | 类型 | 必填 | 说明
---|---|---|---
accesskey_id | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
expires | int | 是 | 参见[用户签名认证](/SIGNATURE.md)
signature | string | 是 | 参见[用户签名认证](/SIGNATURE.md)

### HTTP请求头

无

### 请求参数

无

### 请求示例

```
GET https://api.vzicloud.com/v2/pms/users/refresh_accesskey?accesskey_id=7fdaq37N1135Q1vK2e503HaLYXd1qVj4&expires=1561541184&signature=mF28sM7%2Fv5arqt4gRO7XLipdKDM%3D HTTP/1.1
Host: www.vzicloud.com
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
accesskey_id | string | AccessKeyID，只有两小时有效期
accesskey_secret | string | AccessKeySecret

### 返回示例

```
{
  "accesskey_id": "7fdaq37N1135Q1vK2e503HaLYXd1qVj4",
  "accesskey_secret": "1mXRMQZAWyhukkc5RFR7MPTk4thDrQz9"
}
```