# 创建用户

## 接口描述

用于创建一个用户，如果用户组已存在，则返回错误。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | POST | /v2/frs/user/apps/:app_id/groups/:group_id/users

### PATH参数

参数 | 类型 | 必填 | 说明
---|---|---|---
app_id | int | 是 | PATH中的`:app_id`需要替换为具体的应用ID
group_id | string | 是 | PATH中的`:group_id`需要替换为具体的用户组ID

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
user_id | string | 是 | 用户Id（由数字、字母、下划线组成），长度限制48
user_name | string | 否 | 用户名称
user_info | string | 否 | 用户信息
remark | string | 否 | 用户备注

### 请求示例

```
POST https://api.vzicloud.com/v2/frs/user/apps/2/groups/test_group_01/users?accesskey_id=7hSdi1Gx11552bwS2EqndCm0XZZHBFS0&expires=1563452276&signature=GxdiSE9BAuUq0hynnErQCcZ7g9o%3D HTTP/1.1
Host: www.vzicloud.com
Content-Length: 85
Content-Type: application/json

{"user_id":"guan_xiao_tong","user_name":"关晓彤","user_info":"关晓彤","remark":"无"}
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
app_id | int | 应用Id
group_id | string | 用户组Id
user_id | string | 用户Id
user_name | string | 用户名称
user_info | string | 用户信息
remark | string | 用户备注
create_time | int | 创建时间

### 返回示例

```
{
  "app_id": 2,
  "group_id": "test_group_01",
  "user_id": "guan_xiao_tong",
  "user_name": "关晓彤",
  "user_info": "关晓彤",
  "remark": "无",
  "create_time": 1563445076
}
```