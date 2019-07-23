# 人脸注册（百度云接口）

## 接口描述

用于从人脸库中新增用户，可以设定用户所在组，及用户的人脸图片。该接口与[创建人脸](CREATE.md)的基本目的是一样的，主要是模拟百度云人脸识别接口而设定。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/frs/user/apps/:app_id/faces

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
image | string | 是 | 图片的Base64编码字符串，**切记需要去掉前缀`data:image/jpeg;base64`，并且确保图片大小在2M以内，分辨率小于等于1920(宽)x1080(高)！**
group_id | string | 是 | 用户组Id（由数字、字母、下划线组成），长度限制48，当用户组不存在时自动创建用户组
user_id | string | 是 | 用户Id（由数字、字母、下划线组成），长度限制48，当用户不存在时自动创建用户
group_name | string | 否 | 用户组名称
group_remark | string | 否 | 用户组备注
user_name | string | 否 | 用户名称
user_info | string | 否 | 用户信息
user_remark | string | 否 | 用户备注
action_type | string | 否 | 操作方式，`APPEND`:将人脸图片追加到该用户下；`REPLACE`:清空该用户下的所有人脸后添加该人脸图片。默认为`APPEND`。

### 请求示例

```
POST https://api.vzicloud.com/v2/frs/user/apps/2/faces?accesskey_id=7hJyGena1155WEFT2QXvcOBBOhrHqTf8&expires=1563529909&signature=FyDvNmK3q3eSqC%2FlZsKB6bhb%2Fow%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 586678
Content-Type: application/json

{"group_id":"test_group_01","group_name":"测试分组01","group_remark":"无","user_id":"guan_xiao_tong","user_name":"关晓彤","user_info":"关晓彤","user_remark":"无","image":"/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwc...","image_type":"BASE64"}
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