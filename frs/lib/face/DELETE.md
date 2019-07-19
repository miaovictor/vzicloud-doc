# 删除人脸

## 接口描述

删除指定人脸。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | DELETE | /v2/frs/user/apps/:app_id/groups/:group_id/users/:user_id/faces/:face_id

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
app_id | int | 是 | PATH中的`:app_id`需要替换为具体的应用ID
group_id | string | 是 | PATH中的`:group_id`需要替换为具体的用户组ID
user_id | string | 是 | PATH中的`:user_id`需要替换为具体的用户ID
face_id | string | 是 | PATH中的`:face_id`需要替换为具体的人脸ID

### URL参数

参数 | 类型 | 必填 | 说明
---|---|---|---
accesskey_id | string | 是 | 参见[用户签名认证](/SIGNATURE.md)
expires | int | 是 | 参见[用户签名认证](/SIGNATURE.md)
signature | string | 是 | 参见[用户签名认证](/SIGNATURE.md)

### HTTP请求头

字段 | 值
---|---
Content-Type | application/json

### 请求参数

请求参数以Json格式放置于Body中，如下：

参数 | 类型 | 必填 | 说明 
---|---|---|---
action_type | string | 是 | 图片类型，可选值为`NORMAL`、`USER`、`FACE`、`USER&FACE`

`action_type`四种类型说明：
- **NORMAL**: 只是将人脸从用户的人脸列表中移除，并不会删除人脸数据。
- **USER**: 将人脸从用户的人脸列表中移除，并不会删除人脸数据，但是如果移除后该用户没有其他人脸，则将用户删除。
- **FACE**: 将人脸从用户的人脸列表中移除，并删除人脸数据。
- **USER&FACE**: 将人脸从用户的人脸列表中移除，并删除人脸数据，但是如果移除后该用户没有其他人脸，则将用户删除。

### 请求示例

```
DELETE https://api.vzicloud.com/v2/frs/user/apps/2/groups/test_group_01/users/guan_xiao_tong/faces/f98784e11c8f3d753b18163931dab1be?accesskey_id=7hJyGena1155WEFT2QXvcOBBOhrHqTf8&expires=1563528182&signature=kDTlwbT2wPzL3nVesiA0vFai1uk%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 15
Content-Type: application/json

{"action_type":"USER"}
```

## 返回说明

如果成功，响应状态码为200