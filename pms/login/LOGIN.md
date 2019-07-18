# 账号密码登录

## 接口描述

使用用户名和密码登录。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/pms/users/login

### URL参数

无

### HTTP请求头

字段 | 值
---|---
Content-Type | application/json

### 请求参数

请求参数以Json格式放置于Body中，如下：

参数 | 类型 | 必填 | 说明 
---|---|---|---
username | string | 是 | 用户名，必须大于等于5个字符（允许0-9、a-z、A-Z、下划线，不支持中文）
password | string | 是 | 密码，密码进行MD5后的十六进制字符串（如密码为`123456`，那么计算后为`e10adc3949ba59abbe56e057f20f883e`）

### 请求示例

```
POST https://api.vzicloud.com/v2/pms/users/login HTTP/1.1
Host: www.vzicloud.com
Content-Length: 71
Content-Type: application/json

{"username":"test_ram01","password":"e10adc3949ba59abbe56e057f20f883e"}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
id | int | 用户ID
parent_id | int | 用户父ID
username | string | 用户名
nickname | string | 昵称
email | string | 邮箱地址
phone | string | 手机号码
company | string | 公司名称
type | int | 用户类型，参见[常用值定义](/DEFINE.md)
state | int | 用户状态，参见[常用值定义](/DEFINE.md)
logable | int | 是否可登录，参见[常用值定义](/DEFINE.md)
remark | string | 备注
create_time | int | 创建时间，UNIX时间
accesskey_id | string | AccessKeyID，只有两小时有效期
accesskey_secret | string | AccessKeySecret

### 返回示例

```
{
  "id": 3,
  "parent_id": 2,
  "username": "test_ram01",
  "nickname": "test_ram01",
  "email": "test_ram01@vzenith.com",
  "phone": "18110000001",
  "company": "成都臻识科技发展有限公司",
  "type": 1,
  "state": 0,
  "logable": 0,
  "remark": "成都臻识科技发展有限公司",
  "create_time": 1560837949,
  "accesskey_id": "7fdaq37N1135Q1vK2e503HaLYXd1qVj4",
  "accesskey_secret": "1mXRMQZAWyhukkc5RFR7MPTk4thDrQz9"
}
```