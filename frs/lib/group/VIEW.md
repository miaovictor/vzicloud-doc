# 查看用户组

## 接口描述

获取用户组信息。

## 请求说明

协议 | 方法 | PATH 
---|---|---
HTTPS | GET | /v2/frs/user/apps/:app_id/groups/:group_id

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

无

### 请求参数

无

### 请求示例

```
GET https://api.vzicloud.com/v2/frs/user/apps/2/groups/test_group_01?accesskey_id=7hSdi1Gx11552bwS2EqndCm0XZZHBFS0&expires=1563451451&signature=YLPag4FPNMmF6gN9VGU7BVjUF48%3D HTTP/1.1
Host: www.vzicloud.com
```

## 返回说明

### 返回参数

参数 | 类型 | 说明
---|---|---
app_id | int | 应用Id
group_id | string | 用户组Id
group_name | string | 用户组名称
remark | string | 用户组备注
create_time | int | 创建时间

### 返回示例

```
{
  "app_id": 2,
  "group_id": "test_group_01",
  "group_name": "测试分组01",
  "remark": "",
  "create_time": 1563439927
}
```