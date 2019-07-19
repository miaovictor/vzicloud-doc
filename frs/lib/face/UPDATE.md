# 人脸更新（百度云接口）

## 接口描述

用于对人脸库中指定用户，更新其下的人脸图像。
- 如果指定的用户组不存在，则会返回错误。
- 如果指定的用户不存在时，会返回错误。如果添加了`action_type:REPLACE`,则不会报错，并自动注册该用户，操作结果等同注册新用户。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | PUT | /v2/frs/user/apps/:app_id/faces

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
app_id | int | 是 | PATH中的`:app_id`需要替换为具体的应用ID

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
image_type | string | 是 | 图片类型，固定为`BASE64`
image | string | 是 | 图片的Base64编码字符串，**切记需要去掉前缀`data:image/jpeg;base64`**
group_id | string | 是 | 用户组Id（由数字、字母、下划线组成），长度限制48，当用户组不存在时自动创建用户组
user_id | string | 是 | 用户Id（由数字、字母、下划线组成），长度限制48，当用户不存在时自动创建用户
user_name | string | 否 | 用户名称
user_info | string | 否 | 用户信息
user_remark | string | 否 | 用户备注
action_type | string | 否 | 操作方式，`UPDATE`:会使用新图替换库中该user_id下所有图片, 若user_id不存在则会报错；`REPLACE`:当user_id不存在时, 则会注册这个user_id的用户。默认为`UPDATE`。

### 请求示例

```
PUT https://api.vzicloud.com/v2/frs/user/apps/2/faces?accesskey_id=7hJyGena1155WEFT2QXvcOBBOhrHqTf8&expires=1563529909&signature=FyDvNmK3q3eSqC%2FlZsKB6bhb%2Fow%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 586678
Content-Type: application/json

{"group_id":"test_group_01","user_id":"guan_xiao_tong","user_name":"关晓彤","user_info":"关晓彤","user_remark":"无","image":"/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwc...","image_type":"BASE64"}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
app_id | int | 应用Id
group_id | string | 用户组Id
user_id | string | 用户Id
face_id | string | 人脸Id
location | string | 人脸在图片中的位置信息
format | string | 人脸图片的格式，比如`png`，`jpeg`
create_time | int | 创建时间

### 返回示例

```
{
  "app_id": 2,
  "group_id": "test_group_01",
  "user_id": "guan_xiao_tong",
  "face_id": "e76e8a4c5efdd8cb8fad131f0ac5470e",
  "location": "{\"width\":149,\"left\":131,\"height\":204,\"top\":49}",
  "format": "jpeg",
  "create_time": 1563516170
}
```