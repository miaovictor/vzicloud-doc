# 远程访问设备

## 接口描述

远程访问设备。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | GET | /v2/stp/user/devices/pdns

### PATH参数

无

### URL参数

参数 | 类型 | 必填 | 说明
---|---|---|---
accesskey_id | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
expires | int | 是 | 参见[用户签名认证](/SIGNATURE.md)
signature | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
sn | string | 是 | 设备序列号
ip | string | 否 | 要通过设备访问哪个IP地址，默认是`127.0.0.1`，也就是指定设备本身
port | int | 是 | 要通过设备访问哪个端口
type | string | 否 | 访问类型，可选值有`text`、`url`、`url_login`
userdata | string | 否 | 如果请求方式是`url`或者`url_login`，那么在重定向的URL中，会附件这个参数值，如果为空就不会附加，当前固定为`pdns`
userinfo | string | 否 | 如果请求方式是`url_login`，那么该参数是通过加密的用户名和密码。

### `type`类型

#### `text`
  请求返回的方式，默认的情况下返回的格式是`text`格式，如下所示:
  ```
  120.27.214.100:40059
  ```
#### `json`
  请求返回的方式，默认的情况下返回的格式是`text`格式，如下所示:
  ```
  {
    "host":"120.27.214.100",
    "port":40059
  ```  
#### `url`
  为了方便，我们提供`URL`的形式返回，返回是通过`HTTP`的`302`重定向的形式返回的，这样浏览器可以直接跳转，方便接入和更好的用户体验。如果`type`的类型为`url`，那么，用户可以添加一个`userdata`的字段，这个字段会添加到回复的请求`url`参数里面，这样用户可以判断是否是`PDNS`映射出来的端口，当前`userdata`字段固定为`pdns`。例如：
  ```
  http://120.27.214.100/pdns?accesskey_id=75p9IP2O11M5kuYr2YEgjopRQYbNzZEM&expires=1569321374&signature=XN4LKhc0En93K7mHytTvLStb1sY%3D&sn=2a835e70-324a98ed&port=80&type=url
  ```
#### `url_login`
  如果`type`类型为`url_login`，那么用户还需要添加一个`userinfo`字段，这个字段包含了用户名和密码信息，这样浏览器可以直接跳转并登录到设备页面，加密公式为：
  ```
  userinfo=URLEncode(Base64(AES128_ECB_Eecrypt(MD5(AppKey), "user:pwd")))
  ```
  公式解读：AES采用128密钥进行加密，加密模式为ECB，补位方式为：zeropadding。先对AppKey进行MD5加密，得到一个128位的结果，该结果作为AES加密的密钥。加密的字符串格式为用户名+冒号+密码，即`user:pwd`。对AES加密后的结果进行Base64编码，最后对Base64编码结果进行URLEncode，例如：
  ```
  http://120.27.214.100/pdns?accesskey_id=75p9IP2O11M5kuYr2YEgjopRQYbNzZEM&expires=1569321374&signature=XN4LKhc0En93K7mHytTvLStb1sY%3D&sn=407bb96a-ec7ad3fe&port=80&type=url_login&userdata=pdns&userinfo=40bPBw%2b0ojJ4VPNTuGH0Qg%3d%3d
  ```
  其中，`40bPBw%2b0ojJ4VPNTuGH0Qg%3d%3d`是`admin:admin`加密后的结果。