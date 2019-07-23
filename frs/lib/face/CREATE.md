# 创建人脸

## 接口描述

为用户添加人脸。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/frs/user/apps/:app_id/groups/:group_id/users/:user_id/faces

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
app_id | int | 是 | PATH中的`:app_id`需要替换为具体的应用ID
group_id | string | 是 | PATH中的`:group_id`需要替换为具体的用户组ID
user_id | string | 是 | PATH中的`:user_id`需要替换为具体的用户ID

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
image | string | 是 | 图片的Base64编码字符串，**切记需要去掉前缀`data:image/jpeg;base64`，并且确保图片大小在2M以内，分辨率小于等于1920(宽)x1080(高)！**

### 请求示例

```
POST https://api.vzicloud.com/v2/frs/user/apps/2/groups/test_group_01/users/guan_xiao_tong/faces?accesskey_id=7hJyGena1155WEFT2QXvcOBBOhrHqTf8&expires=1563525973&signature=jVB1KE5Wi8elVO0jD0l%2BpqepXo0%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 586678
Content-Type: application/json

{"image_type":"BASE64","image":"/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDAw..."}
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